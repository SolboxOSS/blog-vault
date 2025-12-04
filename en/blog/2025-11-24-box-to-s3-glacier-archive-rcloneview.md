---
slug: box-to-s3-glacier-archive-rcloneview
title: "Box to S3 + Glacier: Tiered Archives with RcloneView"
authors:
  - tayson
description: "Migrate Box libraries into Amazon S3 hot storage and Glacier Deep Archive for long-term retention, with compare, checksum verification, and scheduled syncs in RcloneView."
keywords:
  - rcloneview
  - box migration
  - s3
  - glacier
  - cloud archive
  - checksum verification
  - scheduler
  - multi cloud
  - rclone
  - tiered storage
  - cloud backup
  - compare sync
  - mount
  - job history
  - visual dashboard
  - gui
  - aws
  - vault
  - compliance
  - long term retention
tags:
  - RcloneView
  - cloud-storage
  - cloud-migration
  - backup
  - s3
  - sync
---

import RvCta from '../src/components/RvCta';

# Box to S3 + Glacier: Tiered Archives with RcloneView

> Move Box libraries into Amazon S3 for active access and Glacier for long-term retention, with visual compares, checksum-verified syncs, and scheduled jobs -- no CLI flags required.

Box is great for collaboration, but long-term retention and large media libraries can get expensive. RcloneView lets you mirror Box folders into S3 buckets for hot access, then push aging data into Glacier classes on a schedule. You get side-by-side compares, logged jobs, and retries without babysitting scripts.

<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />

<!-- truncate -->

## What We Are Solving

- Reduce Box storage spend by tiering cold data into Glacier.
- Keep an always-available S3 copy for active teams while Glacier holds the history.
- Maintain integrity with checksum-verified jobs and an audit trail.

## Connect Box and S3 Remotes Fast

- Add Box and S3 remotes via `+ New Remote`. OAuth and key setup: [add-oath-online-login](/support/howto/remote-storage-connection-settings/add-oath-online-login), [s3](/support/howto/remote-storage-connection-settings/s3).
- Use **Remote Explorer** to sanity-check folder depth and naming before the first sync.
- Optional: mount either remote locally for quick spot checks: [mount-cloud-storage-as-a-local-drive](/support/howto/rcloneview-basic/mount-cloud-storage-as-a-local-drive).

<img src="/support/images/en/howto/rcloneview-basic/mount-from-mount-manager.png" alt="Configure a mount from Mount Manager" class="img-medium img-center" />

## Compare Before You Move

- Run **Compare** between Box and the target S3 prefix to see missing or newer files before committing: [compare-folder-contents](/support/howto/rcloneview-basic/compare-folder-contents).
- Filter by extensions (e.g., PDFs, CAD, media) to scope reviews.
- Save the compare as a job; re-run after each migration wave to confirm parity.

## Build a Two-Tier Pipeline (S3 Hot, Glacier Cold)

- Step 1: Create a **copy** job from Box to S3 for the active tier: [create-sync-jobs](/support/howto/rcloneview-basic/create-sync-jobs). Start with copy for safety; switch to sync after validating results.
- Step 2: Apply S3 lifecycle policies on the bucket to transition objects to Glacier classes after N days. Keep the RcloneView job targeting the hot prefix (e.g., `s3:box-archive/hot/`).
- Step 3: For deep archives, schedule a secondary job to push rarely used folders directly to a Glacier-focused prefix (e.g., `s3:box-archive/cold/`).

## Guardrails: Includes, Excludes, and Checksums

- Exclude transient folders like `~$`, temp exports, or cache dirs using include/exclude rules in the job builder.
- Turn on checksum verification for Box to S3 transfers to ensure byte-level integrity.
- Run a dry-run with the embedded rclone flags before the first full pass.

## Schedule and Observe

- Use the scheduler so migrations run off-hours and resume after interruptions: [execute-manage-job](/support/howto/rcloneview-basic/execute-manage-job).
- Track throughput and any throttling in **Transfer Monitor**: [real-time-transfer-monitoring](/support/howto/rcloneview-basic/real-time-transfer-monitoring).
- Job History provides your audit log -- copies, skips, retries, and errors are all recorded.

## Post-Migration Hygiene

- Re-run **Compare** weekly for a month to ensure no late-arriving files were missed.
- Mount the S3 hot prefix for quick spot checks from Finder or Explorer; unmount when done.
- Export logs for compliance evidence and share with stakeholders.

## Hand-off and Recovery

- Need to roll back a folder? Sync from the S3 hot tier back to Box with a scoped include list.
- To restore a Glacier-only folder, hydrate to S3 (per AWS settings) then point RcloneView at the hydrated prefix.
- Keep presets per business unit so restores are fast and predictable.

RcloneView gives you a visual, repeatable way to exit Box, cut storage costs, and keep compliant archives in AWS. Compare first, copy safely, schedule the rest -- and sleep easy.

<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />
