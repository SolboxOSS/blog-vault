---
slug: warm-standby-disaster-recovery-rcloneview
title: "Warm-Standby Disaster Recovery Across Clouds with RcloneView (S3, Wasabi, R2, OneDrive)"
authors:
  - tayson
description: Build a multi-region warm-standby DR setup with RcloneView and rclone across AWS S3, Wasabi, Cloudflare R2, OneDrive, or Google Drive using scheduled sync, compare, and mount-based failover.
keywords:
  - warm standby
  - disaster recovery
  - multi-region backup
  - rclone s3
  - rcloneview
  - cloud failover
  - compare sync
  - cloudflare r2
  - wasabi s3
tags:
  - RcloneView
  - DR
  - MultiCloud
  - Backup
  - Sync
  - S3
---

import RvCta from '../src/components/RvCta';

# Warm-Standby Disaster Recovery Across Clouds with RcloneView (S3, Wasabi, R2, OneDrive)

> Keep a live copy of production data in another region or cloud and switch within minutes when incidents strike.

Warm-standby DR pairs a primary location (e.g., AWS S3 or OneDrive) with a continuously updated standby (e.g., Cloudflare R2 or Wasabi). RcloneView layers a GUI over rclone so you can schedule steady syncs, validate drift with Compare, and mount the standby for rapid failover—without shell scripts.

<!-- truncate -->

**Relevant docs**

- Create Sync Jobs: https://rcloneview.com/support/howto/rcloneview-basic/create-sync-jobs
- Job Scheduling & Execution: https://rcloneview.com/support/howto/rcloneview-advanced/job-scheduling-and-execution
- Compare and Verify: https://rcloneview.com/support/tutorials/new-window-with-external-rclone
- External rclone flags (S3 & R2): https://rcloneview.com/support/tutorials/new-window-external-rclone-s3-and-r2
- Synology/NAS to cloud patterns: https://rcloneview.com/support/tutorials/synology-nas-cloud-transfer

<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />

## Why warm-standby with RcloneView

- Faster recovery: Standby copies are within minutes/hours of primary, not days.
- Cloud choice: Mix S3, Wasabi, R2, B2, Google Drive, Dropbox, or OneDrive.
- No scripts: Build jobs in a wizard, not YAML/cron.
- Visible drift: Compare highlights mismatches before you need to fail over.
- Safer restores: Mount the standby and copy back without touching production.

## Strategy and architecture

```
[Primary cloud/local/NAS] --(RcloneView scheduled Sync)--> [Standby cloud/region]
                                                \
                                                 --(Weekly Compare)--> [Drift report]
```

- Primary: where apps write (S3 bucket, OneDrive site, GDrive workspace, NAS).
- Standby: another region/provider with versioning (R2/Wasabi/S3/B2).
- Control: RcloneView runs sync on intervals; Compare checks integrity; Mount enables rapid access during failover.

## Prerequisites

- Two remotes configured in RcloneView (e.g., `s3:prod-bucket` and `r2:standby-bucket`).
- Versioning enabled on the standby for rollback safety.
- IAM/API permissions for list/read/write on both sides.
- Bandwidth window for scheduled replication (nightly or hourly).

## Step 1: Build the baseline sync job

1. Create a Sync job: Source = primary, Destination = standby.
2. Use one-way Sync to mirror new/updated files; keep deletes if you want strict parity.
3. Add filters for noisy paths (e.g., cache/temp).
4. Optional performance flags (Advanced Options):

```
--s3-chunk-size=64M --s3-upload-concurrency=8 --checkers=8 --transfers=8
```

5. Save the job so the same settings apply to every run.

## Step 2: Schedule continuous updates

1. Open Scheduler > select the DR job.
2. Choose cadence: hourly for app data, nightly for archives.
3. Enable retries/backoff for flaky links.
4. Turn on logging so you can prove RPO compliance.
5. Add a second scheduled Compare weekly to detect drift early.

<img src="/support/images/en/howto/rcloneview-advanced/create-job-schedule.png" alt="Configure the job scheduler in RcloneView" class="img-medium img-center" />

## Step 3: Verify and monitor

- Use Compare to ensure object counts and checksums match.
- In logs, watch for throttling; tune `--s3-upload-concurrency` if needed.
- Keep versioning on the standby so accidental deletes can be recovered.

## Step 4: Failover playbook

1. Mount the standby: Mount destination remote to a path your app can read.
2. Point workloads to the mounted path or to the standby bucket endpoint.
3. Keep the primary in read-only or offline until incident triage is done.
4. Run a one-time Copy back to primary when it is healthy; disable delete flags during the return to avoid data loss.

```
--dry-run --checksum --no-traverse  # verify before cutover
```

## Tuning tips

- Latency-sensitive apps: lower chunk size and concurrency; schedule during low traffic.
- Compliance: pair with Object Lock (see immutable guide) to block ransomware deletes.
- Cost control: exclude staging/temp folders and enable lifecycle policies after retention windows.
- Multi-cloud: keep two standbys (e.g., R2 + Wasabi) from the same primary using separate jobs.

## Troubleshooting checklist

- Slow replications: reduce `--transfers` and enable bandwidth limits; check peering to standby region.
- Mismatched counts: rerun Compare with `--checksum`; confirm both remotes use versioning.
- Permission errors: ensure API keys allow multipart uploads and listing on both clouds.
- Restore deletes data: use Copy (not Sync) when bringing data back to production.

## Quick-start template

```
Job: Warm-Standby Sync (S3 -> R2)
Source: s3:prod-app-data
Destination: r2:dr-standby
Flags:
  --s3-chunk-size=64M
  --s3-upload-concurrency=8
  --checkers=8
  --transfers=8
Schedule: Hourly at :15 with 2 retries (10m backoff)
Verification: Weekly Compare + email notification on mismatch
Failover: Mount r2:dr-standby and point workloads to the mount
```

Keep your standby warm, tested, and ready so failover is a switch—not a scramble.
