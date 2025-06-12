---
sidebar_position: 2
description: Learn how to use the file explorer panel in RcloneView to manage local and cloud storage.
keywords:
  - rcloneview
  - file explorer
  - cloud file manager
  - remote storage
  - cloud sync
  - file transfer
  - rclone GUI
tags:
  - file-explorer
  - layout
  - UI-guide
  - file-management
  - RcloneView
date: 2025-05-27
author: Jay
---
# File Explorer Panel Overview (deprecated)

This section explains each part of the file explorer panel in RcloneView based on the numbered layout shown in the image.
<img src="/support/images/en/howto/rcloneview-basic/file-explorer-pannel-layout.png" alt="file explorer panel layout" class="img-large img-center" />
### ① Tab Bar

Displays the name and icon of the connected storage remote (e.g., `Local Disk`, `myAwsS3`, `myGoogleDrive`).  
You can switch between active connections using tabs or click `+` to open a new one.

### ② Breadcrumb Path Bar

Shows the current directory path within the selected remote or local source.  
Helps users understand their location and navigate back through the directory hierarchy.

### ③ Panel Toolbar

Provides quick-access action buttons:

- ⭐ **Create Alias (Favorite)** — Save the current folder as a favorite for quick access  
- 🔗 **Mount Folder** — Mount the selected folder as a local drive  
- ⚙️ **Edit Remote Settings** — Modify the configuration of the connected remote  
- ⟳ **Refresh** — Reload the current folder’s contents

### ④ Folder Tree

Displays a collapsible tree view of the directory structure for the selected source (remote or local).  
Enables quick navigation through nested folders.

### ⑤ File/Folder List View

Displays the contents of the selected folder in a detailed, structured view.

Includes:

- Checkboxes for selecting multiple items  
- Icons representing file and folder types  
- Columns for name, modified date, type, and size  

This is the primary workspace for managing and interacting with files.

### ⑥ Summary Footer

Shows a summary of the current folder’s contents:

- Total number of files and folders  
- Combined file size  

Example: `27 files, 48 folders, Total file size: 248.4 MB`  
Helps users quickly assess the volume and size of data in the directory.