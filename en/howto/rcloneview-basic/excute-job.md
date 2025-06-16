---
sidebar_position: 6
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
date: 2025-06-16
author: Jay
---
# Execute Job


### Step 4: Run Job

- Once all settings are complete, click **Run** to start the sync process.

:::important Sync Scheduling. 
To run sync tasks on a scheduled date and time, first **Save to Jobs** to register the sync task as a job. Then, run the **`Job Manager`** to configure the schedule.  

> ⚠️ **Job scheduling is available as a PLUS feature.**   

You will need to purchase a [**PLUS license**](https://rcloneview.com/src/pricing.html) to enable this functionality.
:::

### Simulate: Run a dry run (optional)

You can run a **Dry run** to simulate the sync operation without making any actual changes.

- This preview shows which files will be copied to the **Destination** and which files will be deleted.
- Click **`See details`** to view a full list of operations that would occur (e.g., copy, create, delete) in the destination.

<div class="img-grid-2">
<img src="/support/images/en/howto/rcloneview-basic/sync-dry-run.png" alt="sync dry run" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-dry-run-details.png" alt="sync dry run details" class="img-medium img-center" />
</div>

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


## Job 히스토리 보기
