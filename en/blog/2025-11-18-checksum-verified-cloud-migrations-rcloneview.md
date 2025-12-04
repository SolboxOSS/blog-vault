---
slug: checksum-verified-cloud-migrations-rcloneview
title: "Checksum-Verified Cloud Migrations with RcloneView (Drive, Dropbox, S3, R2)"
authors:
  - tayson
description: Move data between Google Drive, Dropbox, OneDrive, S3, or Cloudflare R2 with checksum validation and drift detection using RcloneView's Sync plus Compare jobs—no command line required.
keywords:
  - checksum migration
  - rclone checksum
  - data integrity
  - rcloneview
  - cloud migration
  - google drive to dropbox
  - s3 to r2
  - compare sync
tags:
  - RcloneView
  - Migration
  - Compare
  - Backup
  - Sync
  - Integrity
---

import RvCta from '../src/components/RvCta';

# Checksum-Verified Cloud Migrations with RcloneView (Drive, Dropbox, S3, R2)

> Move petabytes only once. Use RcloneView to sync, verify with checksums, and catch drift before you switch apps over.

Copying from Google Drive to Dropbox or S3 to R2 is easy—proving every object arrived intact is harder. Rclone has battle-tested checksum and compare modes; RcloneView wraps them in a GUI so you can run integrity-checked migrations with schedules, logs, and zero shell scripts.

<!-- truncate -->

**Relevant docs**

- Create Sync Jobs: https://rcloneview.com/support/howto/rcloneview-basic/create-sync-jobs
- Job Scheduling & Execution: https://rcloneview.com/support/howto/rcloneview-advanced/job-scheduling-and-execution
- Compare and Verify: https://rcloneview.com/support/tutorials/new-window-with-external-rclone
- External rclone flags (S3 & R2): https://rcloneview.com/support/tutorials/new-window-external-rclone-s3-and-r2

<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />

## Why checksum-verified migrations

- Avoid silent corruption: checksums detect bitrot and partial uploads.
- Faster cutovers: Compare highlights mismatches before you flip endpoints.
- Multi-cloud ready: Works across Drive, Dropbox, OneDrive, S3, Wasabi, R2, B2, and NAS.
- Zero scripting: Build, schedule, and re-run jobs visually.

## Migration blueprint

```
[Source cloud/NAS] --(RcloneView Sync with --checksum)--> [Target cloud]
                                           \
                                            --(RcloneView Compare)--> [Drift report]
```

- Stage 1: Baseline Sync with checksum to upload everything once.
- Stage 2: Incremental Syncs on a schedule to shrink cutover window.
- Stage 3: Compare to confirm object counts and hashes match.
- Stage 4: Cutover/Mount the target for production use.

## Prerequisites

- Remotes added in RcloneView for both source and target (e.g., `drive:team`, `dropbox:prod`, `s3:archive`, `r2:mirror`).
- Target has enough quota and, if S3-compatible, versioning enabled for safety.
- API/IAM keys allow list/read/write and, for S3, multipart uploads.

## Step 1: Create a checksum Sync job

1. New Sync job: Source = current system, Destination = target cloud.
2. Open Advanced Options and enable checksum verification:

```
--checksum --checkers=8 --transfers=8 --s3-chunk-size=64M --s3-upload-concurrency=8
```

3. Add include/exclude filters for cache/temp folders.
4. Save the job so reruns keep the same integrity flags.

## Step 2: Schedule incremental runs

1. Open Scheduler > select the migration job.
2. Run nightly or hourly to reduce the final cutover delta.
3. Enable retries/backoff to ride through throttling.
4. Turn on logging for audit and rollback notes.

<img src="/support/images/en/howto/rcloneview-advanced/create-job-schedule.png" alt="Configure the job scheduler in RcloneView" class="img-medium img-center" />

## Step 3: Verify with Compare

- After the baseline, run Compare between source and target with `--checksum` to validate content, not just size.
- Use the weekly scheduled Compare pattern from the scheduler to catch late drift.
- Check the report/logs for mismatches; re-run Sync to fix only the differences.

## Step 4: Cutover safely

1. Freeze writes on the source (maintenance window).
2. Run a final Sync with `--checksum --fast-list` to close the gap.
3. Run Compare one last time; expect zero mismatches.
4. Mount the target in RcloneView so apps/users can validate paths before DNS/endpoint changes.

```
--dry-run --checksum --no-traverse  # quick validation before cutover
```

## Tuning tips

- High latency links: lower `--s3-upload-concurrency`; increase `--s3-chunk-size` for large media.
- Mixed clouds: if a provider lacks checksums, pair `--checksum` with `--size-only` fallback cautiously.
- Bandwidth caps: set `--bwlimit` during business hours; schedule heavier runs overnight.
- Safety net: keep versioning/object lock on the target if ransomware is a concern.

## Troubleshooting checklist

- Mismatch counts: rerun Compare with `--checksum`; verify both sides expose hashes (MD5/SHA/Dropbox content hash).
- Slow verifies: reduce `--checkers` or use `--fast-list` where supported.
- AccessDenied on S3 uploads: ensure multipart and list permissions are granted.
- Deleted files reappear: remove delete flags only after the final cutover if you need strict mirroring.

## Quick-start template

```
Job: Checksum Migration (Drive -> R2)
Source: drive:marketing-hub
Destination: r2:global-marketing
Flags:
  --checksum
  --checkers=8
  --transfers=8
  --s3-chunk-size=64M
  --s3-upload-concurrency=8
Schedule: Nightly at 01:00, 2 retries with 10m backoff
Verification: Weekly Compare with --checksum + email notification on mismatch
Cutover: Final Sync + Compare, then Mount r2:global-marketing for validation
```

Checksum every migration, and you only have to move the data once.
