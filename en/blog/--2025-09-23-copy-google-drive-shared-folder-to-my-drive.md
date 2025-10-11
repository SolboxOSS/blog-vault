---
slug: copy-google-drive-shared-folder-to-my-drive
title: "How to Copy Google Drive Shared Folder to My Drive with RcloneView"
authors:
  - jay
description: Learn how to move Google Drive shared folders into your personal My Drive using RcloneView’s intuitive GUI—drag, preview, and sync without the command line.
keywords:
  - rcloneview
  - google drive
  - shared folder
  - copy to my drive
  - cloud file transfer
  - rclone GUI
  - cloud sync
  - shared files
  - cloud storage management
tags:
  - RcloneView
  - GoogleDrive
  - SharedFolder
  - cloud-file-transfer
  - cloud-sync
---

import CloudSupportGrid from '../src/components/CloudSupportGrid';
import cloudIcons from '../src/contexts/cloudIcons';
import RvCta from '../src/components/RvCta';

# How to Copy Google Drive Shared Folder to My Drive with RcloneView

> Stop juggling shared links and folders. With **RcloneView**, you can copy shared folders from Google Drive into your personal **My Drive** quickly and without command-line headaches.

## Why copy shared folders into My Drive

Shared folders in Google Drive are great for collaboration, but they often sit outside your personal structure. This creates challenges:
<!-- truncate -->

- **Scattered access**: files in “Shared with me” aren’t always searchable like your own content.  
- **Quota management**: moving files into your own drive helps manage storage limits better.  
- **Organization**: keep projects and documents under one consistent folder tree.  
- **Backups**: once inside My Drive, it’s easier to sync or back up with other clouds.

**Understanding Shared Folders in Google Drive**  
- “Shared with me” items don’t belong to your My Drive by default.  
- You can add shortcuts, but those don’t copy the actual files.  
- To fully integrate, you need to copy the content into your own drive.

**Understanding My Drive**  
- Centralized space for your owned files and folders.  
- Counts toward your storage quota.  
- Fully compatible with Rclone and RcloneView transfers and syncs.

> With RcloneView, you can treat shared folders like any other source or destination—copy, compare, and sync them into your own My Drive structure.

<!-- Obsidian note: CTA 컴포넌트 -->
<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />

## Preparation

Before copying:

1. **Access rights** — confirm you have permission to view and copy the shared folder.  
2. **Check My Drive capacity** — ensure your account has enough free space.  
3. **Plan your target folder** — decide where in My Drive the copied content will live.  
4. *(Optional)* **Backup first** — if files are critical, keep an additional backup before reorganizing.

🔍 Helpful guides:  
- [How to Add Google Drive Remote](/support/howto/intro#step-2-adding-remote-storage-google-drive-example)  
- [Quick OAuth Setup](/support/howto/remote-storage-connection-settings/add-oath-online-login#quick-setup-guide)

## Connect Google Drive in RcloneView

1. Open **RcloneView** → click **`+ New Remote`**  
2. Choose **Google Drive** → sign in with your account via OAuth  
3. Name it clearly (e.g., `MyGoogleDrive`)  
4. If needed, add a second **Google Drive remote** for a shared folder with different access (e.g., `SharedDrive`)  
5. Confirm both appear in the Explorer pane

<img src="/support/images/en/tutorials/open-google-drive-and-onedrive.png" alt="Open Google Drive remotes in RcloneView" class="img-medium img-center" />

## Copy shared folders into My Drive

RcloneView supports three practical approaches. Choose based on your needs.

### Drag & Drop
- Browse to the shared folder in one pane, then open your **My Drive** in the other.  
- **Drag and drop** the folder into your chosen My Drive location.  
👉 See more: [Copying Files using Drag and Drop](/support/howto/rcloneview-basic/browse-and-manage-remote-storage#copying-files-using-drag-and-drop)

### Compare & Copy
- Use **Compare** to preview differences between the shared folder and your My Drive.  
- Copy only **new** or **changed** files, reducing duplicates.  
👉 See more: [Compare and Manage Files](/support/howto/rcloneview-basic/compare-folder-contents#compare-results-and-manage-files)

<img src="/support/images/en/howto/rcloneview-basic/compare-display-select.png" alt="Compare shared folder and My Drive contents" class="img-medium img-center" />

### Sync & Scheduled Jobs
- Set the shared folder as **source** and My Drive as **destination**.  
- Run a **dry-run** to preview changes, then execute.  
- Save as a **Job** for recurring syncs if the folder is updated regularly.  
👉 See more:  
- [Synchronize Remote Storages](/support/howto/rcloneview-basic/synchronize-remote-storages)  
- [Create Sync Jobs](/support/howto/rcloneview-basic/create-sync-jobs)  
- [Job Scheduling and Execution](/support/howto/rcloneview-advanced/job-scheduling-and-execution)

<img src="/support/images/en/howto/rcloneview-basic/job-run-click.png" alt="Run a saved sync job in RcloneView" class="img-medium img-center" />

**Pro tips**  
- For very large shared folders, break the copy into subfolders to avoid hitting quotas.  
- Keep the shared folder read-only during initial sync to avoid drift.  
- Use filters to exclude unnecessary cache or temp files.

## Conclusion — Key takeaways

- **Shared folders** live outside My Drive by default; copying them consolidates your content.  
- **RcloneView** provides a clean GUI to handle this—no need for CLI or manual downloads.  
- Choose from **Drag & Drop**, **Compare & Copy**, or **Sync & Scheduled Jobs** depending on your workflow.  
- Always start small, check quotas, and use logs to verify success.

## FAQs

**Q. Does copying count toward my quota?**  
**A.** Yes. Once files are in My Drive, they count against your storage limit.

**Q. Can I keep a shared folder in sync with My Drive?**  
**A.** Yes—use scheduled jobs in RcloneView for ongoing updates.

**Ready to bring shared folders under your control with RcloneView?**  

<CloudSupportGrid />