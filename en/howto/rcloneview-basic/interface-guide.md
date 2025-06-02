---
sidebar_position: 1
description: Explore RcloneView’s interface for syncing and managing local and cloud files.
keywords:
  - rcloneview
  - rclone GUI
  - cloud file manager
  - remote storage management
  - file explorer
  - cloud to cloud transfer
  - file synchronization
tags:
  - RcloneView
  - UI-guide
  - file-explorer
  - Remote-Storage
  - layout
date: 2025-05-27
author: Jay
---

# RcloneView Interface Guide

RcloneView features an intuitive layout that allows users to browse, compare, and transfer files between local storage and cloud remotes. Below is a breakdown of each section with detailed explanations.

<img src="/support/images/en/howto/rcloneview-basic/rcloneview-user-interface.png" alt="rcloneview user interface" class="img-large img-center" />
## ① Title Bar

Displays the application name and standard window control buttons:

- `—`: Minimize
- `□`: Maximize / Restore
- `X`: Exit RcloneView

## ② Main Menu Bar

Main navigation tabs to access core features:

- **`Home`** – Tools for file synchronization and comparison, job scheduling, and multi-window support  
- **`Remote`** – Add, configure, and mount cloud storage remotes  
- **`Settings`** – Manage remote connections, general preferences, and interface layout  
- **`Help`** – Access product support, license activation, feedback, and update checks  

## ③ Toolbar

The toolbar changes dynamically based on the selected menu tab:

  ### When `Home` is selected:

| Button        | Description                                                                           |
| ------------- | ------------------------------------------------------------------------------------- |
| `Sync`        | Synchronize files and folders between selected directories in the two explorer panels |
| `Compare`     | Compare differences between the selected directories in two explorer panels           |
| `Job Manager` | Create and manage recurring synchronization jobs between frequently used remotes      |
| `New Window`  | Open a new RcloneView window to connect to a different Rclone daemon instance         |
 
### When `Remote` is selected:

<img src="/support/images/en/howto/rcloneview-basic/remote-tab-toolbar.png" alt="remote tab toolbar" class="img-medium img-center" />

| Button           | Description                                                                      |
| ---------------- | -------------------------------------------------------------------------------- |
| `New Remote`     | Create a new connection to a cloud storage remote                                |
| `Remote Manager` | View, edit, or delete saved remotes                                              |
| `Mount Manager`  | Mount a remote as a local drive                                                  |
| `Job Manager`    | Create and manage recurring synchronization jobs between frequently used remotes |
  
### When `Settings` is selected:
<img src="/support/images/en/howto/rcloneview-basic/settings-menu-toolbar.png" alt="settings menu toolbar" class="img-medium img-center" />

| Button             | Description                                                                                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------ |
| `Connect Manager`  | Manage and switch between embedded or external Rclone daemon connections                                     |
| `General settings` | Configure application language, file paths, theme, drag-and-drop behavior, embedded Rclone options and more. |
| `Layout`           | Toggle between horizontal and vertical panel layouts for the folder tree and file list view                  |
| `View count`       | Toggle between single-panel and dual-panel file explorer views                                               |

### When `Help` is selected:
<img src="/support/images/en/howto/rcloneview-basic/help-menu-toolbar.png" alt="help menu toolbar" class="img-medium img-center" />

| Button                 | Description                           |
| ---------------------- | ------------------------------------- |
| `Check for Updates`    | Check if a new version is available   |
| `Feedback`             | Submit feedback or report issues      |
| `Homepage`             | Visit the official RcloneView website |
| `Register License Key` | Activate your PLUS license            |

## ④ File Explorer Pannel

Each panel allows you to browse local drives or cloud remotes using a tabbed interface.  
You can open different sources in each panel and transfer files between them easily.

  <img src="/support/images/en/howto/rcloneview-basic/file-explorer-pannel-layout.png" alt="file explorer panel layout" class="img-medium img-center" />
The panel includes the following components:

1. **Tab Bar** – Displays the current connection (e.g., Local Disk, myAwsS3, myGoogleDrive)  
2. **Breadcrumb Path Bar** – Shows the current folder path  
3. **Panel Toolbar** – Includes quick actions:  
	- <img src="/support/icons/alias-icon.png" alt="alias icon" class="inline-icon" /> **Create Alias (Favorite)** — Save the current folder as a favorite for quick access  
	- <img src="/support/icons/mount-icon.png" alt="mount icon" class="inline-icon" />**Mount Folder** — Mount the selected folder as a local drive  
	- <img src="/support/icons/settings-icon.png" alt="settings icon" class="inline-icon" /> **Edit Remote Settings** — Modify the configuration of the connected remote  
	- <img src="/support/icons/refresh-icon.png" alt="refresh icon" class="inline-icon" /> **Refresh** — Reload the current folder’s contents
4. **Folder Tree** – A collapsible folder navigator  
5. **File/Folder List View** – Displays contents with name, type, date modified, and size  
6. **Summary Footer** – Shows total number of files/folders and total file size

## ⑤ Transfer Status Tabs

Displays the status and history of sync or file transfer operations:

| Tab             | Description                                                                                  |
| --------------- | -------------------------------------------------------------------------------------------- |
| **`Transfer`**  | Displays all active transfer jobs in progress, including speed, progress, and remaining time |
| **`Completed`** | Lists all completed sync or copy jobs with details like time, size, and job ID               |
| **`Log`**       | Shows timestamped log entries with timestamps, job types, messages, and status               |
## ⑥ Footer

- **Version Info**: Currently running version of RcloneView (e.g., `RcloneView 0.6.301`)
- **License Info**: Indicates license type (`FREE License` or `PLUS License`)
- **Rclone Connection Info**: Shows the connected rclone instance, server address and OS
  - Example: `Connected to rclone v1.69.1 (http://127.0.0.1:5582, windows)`
