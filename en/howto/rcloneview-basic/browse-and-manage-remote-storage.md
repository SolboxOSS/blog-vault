---
sidebar_position: 2
description: File management guide using RcloneView Explorer to browse, copy, and manage local and cloud storage files.
keywords:
  - rcloneview
  - file management
  - copy files
  - move files
  - drag and drop
  - cloud file transfer
  - cloud storage
  - rclone file explorer
  - cloud to cloud transfer
tags:
  - howto
  - file-management
  - cloud-storage
  - drag-and-drop
  - cloud-file-transfer
date: 2025-05-27
author: Jay
---
# File Management with RcloneView

RcloneView allows you to easily browse, transfer, and organize files between your local disk and multiple cloud storage services using a familiar, Explorer-like interface. 

This guide walks you through:

- Browsing remote storage
- Copying files using drag & drop
- Managing files with the right-click menu

## Browsing Remote Storage

You can open any connected cloud remote and view it like a local folder.

### How to Browse a Remote:

1. Click the **`+`** tab in the **Explorer panel**.
2. Select the remote storage you want to open.
3. The selected remote will open in a new tab, ready for file operations.

<div class="img-grid-2">
<img src="/support/images/en/howto/rcloneview-basic/file-explorer-open-remote.png" alt="file explorer open remote" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/file-explorer-remote-open-complete.png" alt="file explorer remote open complete" class="img-medium img-center" />
</div>

:::tip View Layout
Go to **`Settings > Layout`** to switch between vertical and horizontal views 
<img src="/support/images/en/howto/rcloneview-basic/explorer-view-layout.png" alt="explorer view layout" class="img-small img-left" />
:::

## Copying Files using Drag and Drop

You can transfer files between local and cloud storage using simple drag & drop.
#### Drag and Drop operation

#### Copy Between Two Remotes

Drag files from one remote tab to another in RcloneView to copy them across cloud storages.
<video src="/support/videos/en/howto/rcloneview-basic/rclonview-explorer-drag-and-drop.mp4" class="video-medium video-center" controls muted loop playsinline>
  rclonview explorer drag and drop
</video>
:::tip Multi-File Selection
- Use **`Ctrl + Click`** to select multiple individual files.
- Use **`Shift + Click`** to select a range of files.
:::


:::info Drag & Drop Operation
- **Same remote** = Move operation  
- **Different remotes** = Copy operation
:::

#### Copy from Windows Explorer to Remote in RcloneView
- You can also drag files directly from **Windows File Explorer** into a RcloneView tab to upload them to the cloud storage.
<video src="/support/videos/en/howto/rcloneview-basic/windows-explorer-drag-and-drop.mp4" class="video-medium video-center" controls muted loop playsinline>
  windows explorer drag and drop
</video>

### Managing files with the right-click menu

RcloneView supports full file operations through a convenient right-click menu.

### Available Actions:

-  **Download** – Save file(s) to your local disk  
- **Upload** – Send local file(s) to a cloud remote  
- **Copy / Paste** – Copy files between folders or remotes  
- **Cut / Paste** – Move files to another location  
- **Delete** – Remove files or folders  
- **Rename** – Rename files or folders  
- **New Folder** – Create a new folder  
- **Reload** – Refresh folder contents





