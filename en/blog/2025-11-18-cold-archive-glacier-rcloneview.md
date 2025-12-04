---
slug: tiered-cloud-archive-glacier-rcloneview
title: "Tiered Cloud Backup to S3 Standard, Wasabi, and Glacier Deep Archive with RcloneView"
authors:
  - tayson
description: Build a hot-warm-cold backup pipeline with RcloneView across S3/Wasabi for fast restores and Glacier Deep Archive for ultra-low-cost retention, using scheduled Sync, lifecycle-aware flags, and verification.
keywords:
  - glacier deep archive
  - cold storage
  - tiered backup
  - rclone s3
  - rcloneview
  - wasabi archive
  - lifecycle policy
  - cloud backup
  - archive retention
tags:
  - RcloneView
  - Backup
  - Archive
  - S3
  - Glacier
  - Wasabi
---

import RvCta from '../src/components/RvCta';

# Tiered Cloud Backup to S3 Standard, Wasabi, and Glacier Deep Archive with RcloneView

> Keep recent restores fast and long-term retention cheap: hot in S3 Standard, warm in Wasabi/R2, and archive in Glacier Deep Archivewith RcloneView schedules and lifecycle-friendly flags.

A single storage class rarely fits every file. Design a tiered pipeline: copy fresh data to S3 Standard for rapid access, mirror to a low-cost warm tier (Wasabi/R2) for geo redundancy, and push monthly snapshots to Glacier Deep Archive for compliance retention. RcloneView layers a GUI over rclone so you can schedule Syncs, verify with Compare, and keep lifecycle rules intactno shell scripts.

<!-- truncate -->

**Relevant docs**

- Create Sync Jobs: https://rcloneview.com/support/howto/rcloneview-basic/create-sync-jobs
- Job Scheduling & Execution: https://rcloneview.com/support/howto/rcloneview-advanced/job-scheduling-and-execution
- Compare and Verify: https://rcloneview.com/support/tutorials/new-window-with-external-rclone
- External rclone flags (S3 & R2): https://rcloneview.com/support/tutorials/new-window-external-rclone-s3-and-r2
- Synology/NAS to cloud patterns: https://rcloneview.com/support/tutorials/synology-nas-cloud-transfer

<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />

## Why tiered backup with RcloneView

- Recovery speed: Recent files stay in S3 Standard for low-latency pulls.
- Cost control: Warm copy in Wasabi/R2; deep archive in Glacier for cents per TB-month.
- Resilience: Multi-cloud and multi-region reduce single-provider risk.
- No scripting: Visual jobs, schedules, and logs instead of cron/YAML.
- Proof: Compare jobs surface drift before you need to restore.

## Architecture at a glance

```
[Primary (NAS/Drive/OneDrive)] --(Hourly Sync)--> [S3 Standard hot copy]
                                         \
                                          --(Daily Sync)--> [Wasabi/R2 warm copy]
                                          --(Monthly Copy)--> [Glacier Deep Archive]
```

- Hot: S3 Standard (fast restore).
- Warm: Wasabi or R2 (cheap + egress-friendly for restores).
- Cold: Glacier Deep Archive for 90-365 day retention.

## Prerequisites

- Three remotes configured in RcloneView (e.g., `s3:hot`, `wasabi:warm`, `s3:archive`).
- Versioning on hot/warm buckets; lifecycle rules on `s3:archive` for retention.
- IAM/API permissions: list/read/write + multipart; Glacier restore permissions for cold tier.

## Step 1: Build the hot and warm Sync jobs

1. Create Sync job (Primary -> S3 hot).
2. Add performance flags in Advanced Options:

```
--s3-chunk-size=64M --s3-upload-concurrency=8 --checksum --checkers=8 --transfers=8
```

3. Create a second Sync job (Primary -> Wasabi/R2 warm) using similar flags; add filters to skip temp/cache.
4. Save both jobs.

## Step 2: Add the cold archive Copy job

1. Create a Copy job (S3 hot -> Glacier archive bucket). Use Copy, not Sync, to avoid deletions on archive.
2. In Advanced Options, keep lifecycle-friendly flags minimal:

```
--s3-storage-class=DEEP_ARCHIVE --s3-chunk-size=64M --s3-upload-concurrency=4 --checkers=4
```

3. Ensure the archive bucket has lifecycle to expire old versions after compliance windows.

## Step 3: Schedule everything

- Hot job: Hourly cadence with retries/backoff.
- Warm job: Daily (nightly) to reduce egress impact.
- Cold job: Monthly Copy (first Sunday) for compliance snapshots.
- Add logging and notifications on all jobs.
- Add a weekly Compare (hot vs warm) to catch drift early.

<img src="/support/images/en/howto/rcloneview-advanced/create-job-schedule.png" alt="Configure the job scheduler in RcloneView" class="img-medium img-center" />

## Step 4: Verify integrity

- Run Compare with `--checksum` between hot and warm after the first full sync.
- For the archive, spot-check restores: issue a Glacier retrieval for a test prefix and confirm hashes locally.
- Keep a small canary file (e.g., `canary.txt`) in every tier and check its presence in Compare reports.

## Step 5: Restore playbook

- Fast restores: pull from warm (Wasabi/R2) or hot (S3 Standard) depending on egress/location.
- Deep restores: initiate Glacier restore for the needed prefix; then Copy back to warm/hot.
- Use Mount in RcloneView for browsing before bulk copy to avoid restoring the wrong folders.

```
--dry-run --checksum --no-traverse  # validate before destructive moves
```

## Tuning tips

- Latency/egress sensitive: lower `--transfers` during business hours; raise off-hours.
- Glacier costs: bundle archives monthly; avoid frequent small uploads to reduce PUT and retrieval requests.
- Security: pair hot/warm with Object Lock (see immutable guide) to block ransomware deletes.
- Naming: prefix snapshots with date folders (e.g., `archive/2025-11/`) to simplify lifecycle and restores.

## Troubleshooting checklist

- Restore delays: Glacier retrieval can take hoursplan RPO/RTO accordingly.
- AccessDenied on archive: ensure the IAM role allows `glacier:InitiateJob`/restore for the bucket.
- Drift found: rerun hot/warm Sync; if archive missing objects, re-Copy the delta from hot.
- Costs spiking: enable lifecycle expiration after retention; cap concurrency during peak egress windows.

## Quick-start templates

```
Job: Hot Sync (Primary -> S3 Standard)
Flags: --checksum --checkers=8 --transfers=8 --s3-chunk-size=64M --s3-upload-concurrency=8
Schedule: Hourly at :10, 2 retries (10m backoff)

Job: Warm Sync (Primary -> Wasabi)
Flags: --checksum --checkers=8 --transfers=6 --s3-chunk-size=64M --s3-upload-concurrency=6
Schedule: Nightly at 01:00, 2 retries

Job: Cold Copy (S3 Standard -> Glacier Deep Archive)
Flags: --s3-storage-class=DEEP_ARCHIVE --checkers=4 --transfers=2 --s3-chunk-size=64M --s3-upload-concurrency=4
Schedule: First Sunday monthly at 02:00
Verification: Weekly Compare (S3 hot vs Wasabi warm) with --checksum
Canary: keep /canary.txt in all tiers for health checks
```

Tier once, schedule always, and keep both costs and RPO under control with RcloneView.
