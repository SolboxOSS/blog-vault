---
slug: synology-to-cloud-backup-with-rcloneview
title: "Synology → Cloud, Made Easy: Off-Site Backups & Sync with RcloneView"
authors:
  - jay
description: Protect your Synology NAS with off-site backups to Backblaze, Google Drive, Amazon S3, pCloud, Wasabi, and more—plan, preview, and automate in RcloneView’s GUI.
keywords:
  - rcloneview
  - synology nas backup
  - backblaze b2
  - google drive
  - amazon s3
  - wasabi
  - pcloud
  - cloud backup
  - scheduled sync
  - rclone GUI
tags:
  - RcloneView
  - SynologyNAS
  - CloudBackup
  - S3
  - GoogleDrive
  - Backblaze
  - Wasabi
  - pCloud
---

import CloudSupportGrid from '../src/components/CloudSupportGrid';
import cloudIcons from '../src/contexts/cloudIcons';
import RvCta from '../src/components/RvCta';

# Synology → Cloud, Made Easy: Off-Site Backups & Sync with RcloneView

> Keep a second copy off-site without scripts or terminals. Back up your **Synology NAS** to **Backblaze, Google Drive, Amazon S3, pCloud, Wasabi**, and more—visually, reliably, and on a schedule.

## Introduction — Why push your Synology backups off-site?

A NAS is fantastic for fast, local access—family photos, creative projects, and team shares are only a LAN away. But **on-prem only** has risks: theft, fire, accidental deletion, or multi-drive failures. Adding an **off-site cloud copy** gives you:

<!-- truncate -->

- **Resilience**: survive local disasters with a remote, recoverable copy.  
- **Flexibility**: restore anywhere, even when you’re away from the office/home.  
- **Governance**: combine NAS retention with cloud bucket versioning and policies.

**Synology NAS at a glance**  
- Central storage reachable via **SMB/NFS** (mount as a local folder) or network endpoints like **WebDAV** and **SFTP**.  
- Ideal for always-on backups, media hosting, and team file hubs.

**Cloud destinations at a glance**  
- **Google Drive**: collaboration and sharing in Google Workspace.  
- **Amazon S3 / Wasabi / Backblaze B2**: object storage with buckets, regions, and lifecycle rules.  
- **pCloud**: user-friendly storage with generous file handling.  

**Why send NAS → cloud now?**  
- Create an **off-site safety net**.  
- **Standardize** backups to a single destination (or multi-cloud).  
- Leverage **policies & versioning** available on many cloud platforms.

<!-- Obsidian note: CTA 컴포넌트 -->
<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />
## Step 1 — Preparation

Before you begin:

1. **Choose your scope** — which shared folders on Synology (e.g., `/photo`, `/projects`, `/backup`) will go to the cloud?  
2. **Confirm cloud capacity** — ensure the target account or bucket has room (plus headroom for versions).  
3. **Pick a NAS connection method**  
   - **Local path**: mount the NAS share via **SMB/NFS** on your OS and use it as **Local** in RcloneView.  
   - **WebDAV**: enable Synology’s **WebDAV Server** and connect with WebDAV in RcloneView.  
   - **SFTP**: enable SSH/SFTP on Synology and connect with **SFTP**.  
4. **Pick your cloud** — Google Drive, Amazon S3/Wasabi, Backblaze B2, pCloud, etc.  
5. **Decide cadence** — one-off archive, periodic sync, or **nightly scheduled jobs**.  
6. **Pilot first** — run a small test to validate paths, permissions, and throughput.

🔍 Helpful overview:
- [Cloud ↔ Synology tutorial](/support/tutorials/synology-nas-cloud-transfer)


## 3) Step 2 — Wire up connections in RcloneView

RcloneView wraps rclone’s configuration into a guided, click-through flow.

1. Open **RcloneView** → click **`+ New Remote`**  
2. **Add Synology (source)** via one of:  
   - **Local**: pick your mounted NAS folder (e.g., `Z:\NAS\Projects` or `/Volumes/NAS/Projects`)  
   - **WebDAV**: use Synology’s WebDAV endpoint/credentials → name it (e.g., `NAS-WebDAV`)  
   - **SFTP**: host/IP, port, and account → name it (e.g., `NAS-SFTP`)  
3. **Add Cloud (destination)**, for example:  
   - **Google Drive**: OAuth login → name it `MyGoogleDrive`  
   - **Amazon S3 / Wasabi**: **S3** provider → access key/secret, region, bucket → name it `MyS3` / `MyWasabi`  
   - **Backblaze B2**: **B2** provider (or S3-compatible endpoint if applicable) → name it `MyB2`  
   - **pCloud**: sign-in/token flow → name it `MyPcloud`  
4. Confirm both appear side-by-side in the Explorer pane.

🔍 Helpful guides:  
- [Quick OAuth Setup (Google Drive, etc.)](/support/howto/remote-storage-connection-settings/add-oath-online-login#quick-setup-guide)
- [Add S3 Remote (Amazon S3/Wasabi)](/support/howto/remote-storage-connection-settings/s3)
- [Cloud ↔ Synology tutorial](/support/tutorials/synology-nas-cloud-transfer)

<img src="/support/images/en/tutorials/synology-nas-webdav-and-google-drive.png" alt="synology nas webdav and google drive" class="img-medium img-center" />

## 4) Step 3 — Run the backup/sync (three practical methods)

RcloneView offers three straightforward approaches. Start small, then scale with confidence.

### A) Drag & Drop (manual copy)
- Open **Synology (Local/WebDAV/SFTP)** on one side and your **cloud** on the other, then **drag folders/files across**.  
- Great for selective moves and quick wins.  

👉 See more: [Copying Files using Drag and Drop](/support/howto/rcloneview-basic/browse-and-manage-remote-storage#copying-files-using-drag-and-drop)

### B) Compare & Copy (preview changes)
- Run **Compare** to see what’s new/changed on the NAS vs. your cloud bucket/drive.  
- Copy only deltas—fewer surprises, faster runs.  

👉 See more: [Compare and Manage Files](/support/howto/rcloneview-basic/compare-folder-contents#compare-results-and-manage-files)

<img src="/support/images/en/howto/rcloneview-basic/compare-display-select.png" alt="Compare results highlighting changed files" class="img-medium img-center" />

### C) Sync & Scheduled Jobs (automate)
- Use **Sync** to mirror selected NAS folders into your cloud destination.  
- **Dry-run** first, then save as a reusable **Job** and add a schedule (nightly/weekly).  

👉 See more:
- [Synchronize Remote Storages](/support/howto/rcloneview-basic/synchronize-remote-storages)
- [Create Sync Jobs](/support/howto/rcloneview-basic/create-sync-jobs)
- [Job Scheduling and Execution](/support/howto/rcloneview-advanced/job-scheduling-and-execution)

<img src="/support/images/en/howto/rcloneview-basic/job-run-click.png" alt="Running a saved job in RcloneView" class="img-medium img-center" />

**Pro tips**
- For **S3-type clouds** (S3/Wasabi/B2 S3-compatible), pre-create buckets and pick the correct region.  
- Enable **versioning** on supported buckets for safer rollbacks.  
- Keep NAS sources **read-only during cutover** to prevent drift.  
- Use filters to exclude cache/temp folders from backups.


## 5) Conclusion — Key takeaways & extra tips

- **Why do this**: a durable off-site safety net, faster disaster recovery options, and unified retention.  
- **How it works**: RcloneView connects your Synology NAS and cloud destinations, then lets you **Drag & Drop**, **Compare**, or **Sync**—with **scheduling** for hands-off backups.  
- **Scale safely**: pilot first, respect provider quotas, and monitor job logs for a clean audit trail.


## FAQs

**Q. Can I back up to multiple clouds?**  
**A.** Yes—add multiple destinations (e.g., S3 and Google Drive) and create separate jobs or schedules for each.

**Q. Do I need the command line?**  
**A.** No. RcloneView is a full GUI—configure remotes, preview changes, run syncs, and schedule jobs without CLI.


**Ready to put your Synology backups on autopilot—off-site and under control?**  

<CloudSupportGrid />
