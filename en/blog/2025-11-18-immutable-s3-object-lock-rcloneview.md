---
slug: immutable-backups-s3-object-lock-rcloneview
title: "Immutable, Ransomware-Proof Backups with S3 Object Lock in RcloneView"
authors:
  - tayson
description: Use RcloneView and rclone's S3 Object Lock flags to build immutable, ransomware-proof backups on AWS S3, Wasabi, Backblaze B2, or Cloudflare R2, with scheduling, verification, and speedy restores.
keywords:
  - s3 object lock
  - immutable backups
  - ransomware protection
  - rclone s3
  - rcloneview
  - wasabi object lock
  - cloud backup immutability
  - compliance backup
tags:
  - RcloneView
  - Backup
  - Security
  - S3
  - Wasabi
  - R2
---

import RvCta from '../src/components/RvCta';

# Immutable, Ransomware-Proof Backups with S3 Object Lock in RcloneView

> Stop worrying about ransomware rollbacks. Combine S3 Object Lock with RcloneView's scheduler to keep backups untouchable.

Immutable storage keeps attackers (or accidents) from deleting or overwriting your backups before you can recover. S3 Object Lock is available on AWS S3, Wasabi, Backblaze B2, and Cloudflare R2, and rclone exposes it via flags that RcloneView can pass through in a job. This guide shows how to enable Object Lock on the bucket, wire it up in RcloneView, schedule protected jobs, and verify retention without touching the CLI.

<!-- truncate -->

**Relevant docs**

- Create Sync Jobs: https://rcloneview.com/support/howto/rcloneview-basic/create-sync-jobs
- Job Scheduling & Execution: https://rcloneview.com/support/howto/rcloneview-advanced/job-scheduling-and-execution
- Compare and Verify: https://rcloneview.com/support/tutorials/new-window-with-external-rclone
- Rclone S3 flags (Object Lock): https://rcloneview.com/support/tutorials/new-window-external-rclone-s3-and-r2

<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />

## Why Object Lock + RcloneView

- Immutable copies: Retention dates block deletes/overwrites for the specified window.
- Cloud choice: Works on S3, Wasabi, R2, B2, and S3-compatible NAS gateways.
- No scripting: RcloneView passes rclone's Object Lock flags, schedules runs, and keeps logs.
- Fast checks: Use Compare to confirm the destination matches and shows retained versions.
- Easy restores: Mount or Sync back from the locked bucket without changing retention.

## Prerequisites

- An S3-compatible bucket created with Object Lock enabled at creation time.
- Versioning enabled on that bucket (required for Object Lock).
- RcloneView installed with an S3 remote already connected.
- An IAM/API user with permissions for `PutObject` and `PutObjectRetention`.

## Step 1: Enable Object Lock on the bucket

1. Create the bucket with Object Lock turned on (cannot be toggled later). On AWS S3, check "Enable Object Lock". On Wasabi/R2/B2, choose the Object Lock option during bucket creation.
2. Turn on versioning for that bucket.
3. Decide your default retention: Governance (easier overrides) or Compliance (no overrides), and retention duration (e.g., 30-90 days).

## Step 2: Add Object Lock flags in RcloneView

You can pass rclone Object Lock flags when building a job in RcloneView:

- Mode: `--s3-object-lock-mode=COMPLIANCE` (or `GOVERNANCE`)
- Default retention period: `--s3-object-lock-retain-until-days=45`
- Optional legal hold per object: `--s3-object-lock-legal-hold`

Example advanced options string:

```
--s3-object-lock-mode=COMPLIANCE --s3-object-lock-retain-until-days=45 --s3-chunk-size=64M --s3-upload-concurrency=8
```

In RcloneView:

1. New Sync job > pick your source (local, NAS, or cloud) and destination (Object Lock bucket).
2. Open Advanced Options and paste the flags above.
3. Save the job to keep these defaults for every run.

## Step 3: Schedule immutable backups

1. Go to Scheduler and choose your job.
2. Set Daily or Hourly cadence; add retries if bandwidth is flaky.
3. Enable logging and notifications so you know when a run fails.
4. Keep a second schedule for weekly Compare to validate retained objects.

RcloneView will push the Object Lock parameters on every scheduled run, so new objects inherit retention automatically.

## Step 4: Verify retention and integrity

- Use Compare to verify object counts and checksums after uploads.
- In the S3 console (or RcloneView logs), check that objects show `Compliance`/`Governance` and the expected Retain Until date.
- Try deleting a test file from the destination; it should be blocked until the retention window expires.

## Step 5: Restore from immutable backups

When you need to recover:

1. Create a new job: Destination (Object Lock bucket) -> Source (recovery location), and run Sync/Copy.
2. For ad-hoc restores, use Mount to browse the locked bucket and drag files out.
3. Keep Object Lock flags disabled on restore jobs so you do not change retention.

## Best practices and tuning

- Set retention long enough for detection plus investigation (e.g., 30-90 days).
- Use Governance mode for flexibility in labs; Compliance for production and regulated data.
- Enable multi-part tuning (`--s3-chunk-size`, `--s3-upload-concurrency`) for large media or VM images.
- Keep at least two regions or providers (e.g., Wasabi + R2) and rotate schedules.
- Monitor costs: Object Lock keeps all versions, so pair with lifecycle rules after retention expires.

## Troubleshooting checklist

- Upload fails with AccessDenied: ensure the IAM role allows `PutObjectRetention`.
- Objects not locked: confirm the bucket was created with Object Lock and versioning is On.
- Slow transfers: lower `--s3-upload-concurrency` or use bandwidth limits when peering is weak.
- Restore deletes live data: use Copy instead of Sync when pulling from the locked bucket.

## Quick-start template

```
Job: Immutable Backup to Wasabi
Source: E:\Projects
Destination: wasabi:prod-immutable
Flags:
  --s3-object-lock-mode=COMPLIANCE
  --s3-object-lock-retain-until-days=60
  --s3-chunk-size=64M
  --s3-upload-concurrency=8
Schedule: Daily at 02:00, 2 retries with 10m backoff
Verification: Weekly Compare + email notification on mismatch
```

Lock your backups once, and let RcloneView keep them safe on autopilot.
