---
sidebar_position: 4
description: This is sample Post for writer
keywords:
  - rcloneview
  - howto
  - cloud
  - sync
  - rclone
tags:
  - RcloneView
  - howto
  - Cloud
  - Sync
date: 2025-06-04
author: Jay
---
# Synchronize Remote Storages Instantly

Use RcloneView's **`Sync`** feature to instantly mirror folders between cloud remotes or local storage.  

This guide walks you through setting up and running a sync operation.
## Select source and destination folders

To begin a sync operation, you need to define the **Source** and **Destination** folders.

- In the **Explorer** panel, open two tabs:
	- The folder selected on the **left tab** becomes the **Source**
	- The folder selected on the **right tab** becomes the **Destination**

- You can also enter folder paths directly using the **Path Bar** at the top of each tab.
- These settings can later be adjusted in the **Sync** configuration window if needed.

Once the folders are selected, click the **`Sync`** button in the top **`Home`** menu to proceed.
<img src="/support/images/en/howto/rcloneview-basic/sync-remote-folder-select.png" alt="sync remote folder select" class="img-medium img-center" />
## Run sync operation

After selecting the source and destination folders, you can configure and run your sync.

### Step 1: Verify folder paths

- In the **`Configure Storage`** step, review the selected source and destination folders.
- Make sure both are correctly set before clicking **Next**.

:::caution How sync works
RcloneView’s sync is **one-directional sync(=`Modifying destination only`)**.  
It mirrors the contents of the **Source** to the **Destination**.  
Any existing files on the destination that do not exist in the source may be **deleted**.  

Currently, Rclone officially supports **one-directional sync**.  
**Bidirectional sync(`=Bidirection`)** is available as a beta feature and is not officially supported,  
so errors may occur more frequently. It is not recommended for production use.
:::

### Step 2: Advanced settings (optional)

  - Advanced Settings include options for:
	  - Transfer performance
	  - Connection method
	  - Error handling behavior

> 💡 We recommend using the default values unless you need custom behavior.
> 📘 For details, see [the Sync Advanced Settings](../rcloneview-advanced/sync-advanced-settings.md).

### Step 3: Filter files and folders (optional)

- RcloneView applies basic filters by default for services like Google Docs or Box Docs.
- You can add more file types or folders to exclude from the sync.

> 📘 For details, see [the Sync Filtering Settings](../rcloneview-advanced/sync-filtering-settings.md).
  
  
### Step 4: Run sync

- Once all settings are complete, click **Run** to start the sync process.

<div class="img-grid-3">
<img src="/support/images/en/howto/rcloneview-basic/sync-configure-storage.png" alt="sync configure storage" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-advanced-settings.png" alt="sync advanced settings" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-filtering-settings.png" alt="sync filtering settings" class="img-medium img-center" />
</div>

:::important Sync Scheduling
Sync를 특정날짜/시간에 주기적으로 수행되도록 스케쥴링하려면 Save to Jobs 로 Sync 타스크를 Job으로 저장한후 Job Manager에서 스케쥴링 할 수 있습니다.{{링크 달기}}
단, Job Scheduling은 PLUS 기능으로 PLUS 라이선스 구입이 필요합니다. {{링크달기}}
:::
## Monitor sync results

You can check the progress and results of sync operations in real time.

### Transfer status (in progress)

- During sync, open the **`Transfer`** tab to view real-time progress of each file.
- Click the **+** icon to expand and monitor individual file transfers.
<img src="/support/images/en/howto/rcloneview-basic/sync-transfer-window.png" alt="sync transfer window" class="img-medium img-center" />

### Completed jobs (after sync)

- Once the sync is finished, go to the **`Completed`** tab to view the results.
- Click the **+** icon to see file-level details of each completed job.
<img src="/support/images/en/howto/rcloneview-basic/sync-completed-window.png" alt="sync completed window" class="img-medium img-center" />
:::tip Quickly open synced remotes
In the **`Completed`** tab, you can double-click any completed job to open both the source and destination folders in the Explorer panel.  
This makes it easy to review the synced folders immediately.
:::

### Completion notification alarm (Windows)

After the sync is complete, a notification popup will appear in the Windows system tray, showing a summary of the sync operation.

  - You can click **`See details`** to view a full breakdown of the results.
<img src="/support/images/en/howto/rcloneview-basic/sync-completed-windows-alarm.png" alt="sync completed windows alarm" class="img-medium img-center" />
:::tip See the alarm messages on Windows notification
If you miss the popup, you can still check the sync alert by clicking the **notification icon** in the **Windows system tray**.
<img src="/support/images/en/howto/rcloneview-basic/click-windows-alarm-notification.png" alt="click windows alarm notification" class="img-small img-left" />
:::

## Run a dry run (optional simulation)

You can run a **Dry run** to simulate the sync operation without making any actual changes.

- This preview shows which files will be copied to the **Destination** and which files will be deleted.
- Click **`See details`** to view a full list of operations that would occur (e.g., copy, create, delete) in the destination.

<div class="img-grid-2">
<img src="/support/images/en/howto/rcloneview-basic/sync-dry-run.png" alt="sync dry run" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-dry-run-details.png" alt="sync dry run details" class="img-medium img-center" />
</div>


## Save sync operation as a Job

If you regularly perform the same sync task, you can save it as a **Job** for easy reuse.

- Click **`Save to Jobs`** after configuring your sync.
- You can later run the saved Job from the **`Job Manager`** with one click.

<img src="/support/images/en/howto/rcloneview-basic/save-sync-to-jobs.png" alt="save sync to jobs" class="img-medium img-center" />
You can view and run saved jobs by clicking the **`Job Manager`** toolbar in the Home menu.
<img src="/support/images/en/howto/rcloneview-basic/verify-job-in-job-manager.png" alt="verify job in job manager" class="img-medium img-center" />
