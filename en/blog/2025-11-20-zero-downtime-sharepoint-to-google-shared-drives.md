---
slug: zero-downtime-sharepoint-to-google-shared-drives-rcloneview
title: "Zero-Downtime SharePoint to Google Shared Drives Migration with RcloneView"
authors:
  - tayson
description: Lift Microsoft 365 SharePoint Online libraries into Google Shared Drives without interrupting users by combining RcloneView's multi-cloud Explorer, Compare previews, Sync jobs, and scheduler-driven delta passes.
keywords:
  - sharepoint to google drive
  - google shared drive migration
  - rcloneview
  - zero downtime transfer
  - microsoft 365 to workspace
  - rclone compare
  - multi cloud sync
  - scheduler automation
  - sharepoint cutover plan
  - cloud migration blueprint
tags:
  - RcloneView
  - SharePoint
  - GoogleDrive
  - Migration
  - Scheduler
---

import RvCta from '../src/components/RvCta';

# Zero-Downtime SharePoint to Google Shared Drives Migration with RcloneView

> Keep designers, finance, and project teams working in SharePoint while you hydrate Google Shared Drives in the background--then flip the switch in one cutover window.

SharePoint Online libraries are often packed with permission-heavy folders, document sets, and regional data controls. At the same time, Google Workspace Shared Drives promise simpler collaboration and storage quotas, but the native movers rarely honor metadata, delta windows, or throttling. RcloneView wraps rclone's SharePoint and Google Drive backends in a GUI, so you can plan multi-cloud migrations with staged Compare runs, Sync + Copy jobs, mount-based QA, and scheduler-based delta passes.

<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />

<!-- truncate -->

## Why Plan a Zero-Downtime SharePoint -> Google Cutover

- **Distributed teams can't pause** -- marketing assets, PMOs, and contracts need continuous access while the new Shared Drive is filling.
- **Granular permissions** -- SharePoint libraries mix Teams-connected folders and standalone document centers; you need a repeatable way to rebuild them inside Shared Drives with clear audit logs.
- **API hygiene and throttling** -- Microsoft and Google enforce concurrency limits that are easier to respect when a scheduler orchestrates transfers instead of ad-hoc scripts.

A zero-downtime strategy means running multi-phase syncs while both platforms stay online, then cutting over after the final delta.

## Migration Blueprint: Multi-Cloud Control Panel

1. **Connect both sides** using [Remote Manager](/support/howto/rcloneview-basic/remote-manager) along with the provider guides for [SharePoint for Business](/support/howto/remote-storage-connection-settings/connect-using-cli/add-sharepoint-for-business) and [Google Shared Drives](/support/howto/remote-storage-connection-settings/connect-using-cli/add-google-shared-drive). RcloneView isolates OAuth tokens per tenant and stores them with the protections described in [General Settings](/support/howto/rcloneview-basic/general-settings).
2. **Organize Explorer panes** so each pane references a matching library vs. Shared Drive. Color labels and workspace folders keep multi-team migrations tidy.
3. **Templates for jobs** come from [Create Sync Jobs](/support/howto/rcloneview-basic/create-sync-jobs) and [Synchronize Remote Storages](/support/howto/rcloneview-basic/synchronize-remote-storages). Copy jobs seed the target; Sync jobs handle bidirectional clean-up; Compare runs validate.
4. **Mounts for QA** follow [Mount cloud storage as a local drive](/support/howto/rcloneview-basic/mount-cloud-storage-as-a-local-drive), letting power users preview content inside Finder or Explorer before cutover.
5. **Schedulers + monitoring** rely on [Job scheduling and execution](/support/howto/rcloneview-advanced/job-scheduling-and-execution) and [Real-time transfer monitoring](/support/howto/rcloneview-basic/real-time-transfer-monitoring) to keep delta runs predictable.

## Step 1 -- Harden Connectors & Metadata

- Label every remote (`sp-marketing`, `sp-pmo`, `gdrive-regional-apac`) and restrict the root path to the specific library. This keeps remote browsing fast inside [Browse and manage remote storage](/support/howto/rcloneview-basic/browse-and-manage-remote-storage).
- Enable Config Password + OS keychain storage in [General Settings](/support/howto/rcloneview-basic/general-settings) before sharing the project file with other engineers.
- Mirror permission documents: export SharePoint's sharing matrix and attach it to the RcloneView job memo so auditors see which folders map to which Shared Drive.

## Step 2 -- Baseline with Compare Runs

1. Open the dual-pane Explorer, point the left side at SharePoint, right side at the empty Shared Drive.
2. Use [Compare folder contents](/support/howto/rcloneview-basic/compare-folder-contents) to detect size, checksum, and timestamp deltas.
3. Export the Compare report for stakeholders so they know the seed volume before data starts moving.

<img src="/support/images/en/howto/rcloneview-basic/compare-display-select.png" alt="Compare SharePoint library to Google Shared Drive before migrating" class="img-medium img-center" />

Baseline Compare snapshots give you a forensic record of the original state and help identify stale subsites you might archive instead of moving.

## Step 3 -- Stage Copy + Sync Jobs

- Create a **Copy** job per business unit to hydrate the Shared Drive without deleting anything on SharePoint. Reference [Create Sync Jobs](/support/howto/rcloneview-basic/create-sync-jobs) for bandwidth caps, retries, and checksum verification.
- Add advanced flags like `--drive-import-formats` where you need Office docs saved as Google formats, or leave them untouched for regulated teams that must keep original metadata.
- Set `--backup-dir` on Sync jobs targeting a temporary bucket (e.g., Wasabi) so removed SharePoint files stay recoverable during the transition.

Run the Copy job manually once, review [Real-time transfer monitoring](/support/howto/rcloneview-basic/real-time-transfer-monitoring) graphs, and note throughput + API usage for capacity planning.

## Step 4 -- Automate Delta Windows with Scheduler

Open Scheduler, enable it globally, then assign cadences per job:

- **Intraday mini-syncs** targeting folders with active collaboration (Creative, Bid teams). Limit transfers/checkers to avoid SharePoint throttles.
- **Nightly full sync** that sweeps every library during off-hours, ensuring the Shared Drive is nearly caught up before cutover.
- **Daily Compare-only job** that posts drift alerts to chat/email when users create new folders after freeze notices go out.

<img src="/support/images/en/howto/rcloneview-advanced/create-job-schedule.png" alt="Schedule staged SharePoint to Google migration jobs inside RcloneView" class="img-medium img-center" />

Because Scheduler lives inside RcloneView, you do not need Task Scheduler or cron; the app handles retries, missed-run notifications, and reboots automatically.

## Step 5 -- Cutover Day Checklist

1. **Freeze writes** on SharePoint (communicate via Teams/Slack) but keep the site online for read-only needs.
2. Run the final Sync + Compare job set. Use the Compare diff to confirm only a handful of files changed since the last delta.
3. Mount the new Shared Drive with [Mount cloud storage as a local drive](/support/howto/rcloneview-basic/mount-cloud-storage-as-a-local-drive) and have business owners spot-check complex folder trees.
4. Update bookmarks, shortcuts, and Workspace access groups. Keep the SharePoint remote available for two weeks in read-only mode in case late files appear.

## Post-Migration QA & Mount Operations

Mount Manager lets engineers, finance, or creative leads open the new Shared Drives (or the legacy SharePoint remote) as read-only drives for auditing and training. Pair mounts with [Execute and manage job](/support/howto/rcloneview-basic/execute-manage-job) exports so you can attach execution logs, timestamps, and job IDs to the migration ticket.

## Project Timeline Playbook

| Phase | RcloneView action | Outcome |
| --- | --- | --- |
| Week 1 | Connect remotes, baseline Compare, create Copy jobs | Inventory of each library + seeded Shared Drives |
| Week 2 | Nightly Scheduler delta + Weekly Compare report | Continuous updates with drift visibility |
| Week 3 | Pilot mounts, permissions validation, user training | Stakeholders preview Google Shared Drives safely |
| Cutover week | SharePoint freeze, final Sync/Compare, Shared Drive go-live | Minutes of downtime with signed validation logs |
| 2 weeks after | Scheduled Compare on legacy remote + optional archival Copy to S3/Wasabi | Proof that no files were missed before decommissioning |

## FAQ

**Does RcloneView preserve metadata like versions or author names?**  
Rclone/rcloneview copies file contents, timestamps, and hashes. For version history, export SharePoint audit reports and store them next to the migration job logs. Use Shared Drive activity dashboards post-cutover for ongoing edits.

**What if Microsoft throttles API calls mid-transfer?**  
Reduce `--transfers` and `--checkers` in the job configuration, enable bandwidth caps, and let Scheduler retry during quieter windows. Logs in [Execute and manage job](/support/howto/rcloneview-basic/execute-manage-job) document the adjustments for compliance teams.

**Can I keep both SharePoint and Google in sync long term?**  
Yes. Leave the Sync job active with weekly cadence, or split Explorer panes into [Multi-window operations](/support/howto/rcloneview-advanced/multi-window) if specific departments need bi-directional updates for an extended coexistence period.

RcloneView turns multi-cloud migrations into a predictable playbook: set up remotes, preview differences, stage Copy + Sync jobs, automate deltas, and mount for QA. Your teams stay productive on SharePoint until the exact moment you redirect them to Google Shared Drives.


