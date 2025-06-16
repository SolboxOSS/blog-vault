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


<div class="img-grid-3">
<img src="/support/images/en/howto/rcloneview-basic/sync-configure-storage.png" alt="sync configure storage" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-advanced-settings.png" alt="sync advanced settings" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-filtering-settings.png" alt="sync filtering settings" class="img-medium img-center" />
</div>

### Step 1: Verify folder paths

- In the **`Configure Storage`** step, review the selected source and destination folders.
- Make sure both are correctly set before clicking **Next**.

:::caution How sync works
RcloneView Sync make source and dest identical.  
This means **`modifying destination only`**.  
- The contents of the **source** folder are mirrored to the **destination**.  
- Any existing files in the destination that do not exist in the source will be **deleted**.  

👍 **Important:** Rclone officially supports **one-directional sync** only.  
⚠️ **Bidirectional sync (=Bidirection)** is available as a **beta feature** and is not officially supported.  It may cause unexpected behavior or errors, so it is **not recommended for production use**.
:::

<details>
<summary>Configure Storage Details</summary>

<img src="/support/images/en/howto/rcloneview-basic/sync-config-storage-details.png" alt="sync config storage details" class="img-medium img-center" />

1. **Select the source folder**.   
 - Click the folder icon in the left panel to choose the source.  
2. **Select the destination folder**. 
- Click the folder icon in the right panel to choose the destination.  
3. **Add additional destinations** (optional). 
- Click the **Add Destination** button to sync to multiple destinations at once.  You can configure **1:N sync** if needed.  
4. **Choose the sync direction**. 
 - **Modifying destination only**: Syncs from source to destination. Updates or deletes destination content to match the source.  
 - **Bidirection** (Beta): Compares both folders and syncs changes in both directions.  
⚠️ This mode may overwrite new files unintentionally, so use with caution.  
5. **Create empty directories (optional)**.   
- If enabled, any source directories that contain no files will be recreated as empty folders in the destination.  

:::caution Using Bidirectional Sync in RcloneView
RcloneView uses `bisync` (a beta command in rclone) to perform bidirectional sync.    
Since this feature is still **experimental**, we recommend reviewing the official [user manual](https://rclone.org/bisync/) — especially the [Limitations](https://rclone.org/bisync/#limitations) section — before enabling it.

Using bisync incorrectly may result in data loss. Please use with caution.
:::


</details>

### Step 2: Advanced Settings (optional)

  - Advanced Settings include options for:
	  - Transfer performance
	  - Connection method
	  - Error handling behavior

> 💡 We recommend using the default values unless you need custom behavior.

<details>
<summary>Advanced Settings Details</summary>

<img src="/support/images/en/howto/rcloneview-basic/sync-advanced-settings-details.png" alt="sync advanced settings details" class="img-medium img-center" /> 
### Performance
1. **`Number of file transfers`**:   
   The number of file transfers to run in parallel. It can sometimes be useful to set this to a smaller number if the remote is giving a lot of timeouts or bigger if you have lots of bandwidth and a fast remote.  
2. **`Number of multi thread transfers`**:  
   When using multi thread transfers this sets the number of streams to use. Set to `0` to disable multi thread transfers (Default 4). When transferring files above 256MB to capable backends, rclone will use multiple threads to transfer the file.  
3. **`Number of equaility checkers`**:  
   checkers do the equality checking of files during a sync. For some storage systems (e.g. S3, Swift, Dropbox) this can take a significant amount of time so they are run in parallel. The default is to run 8 checkers in parallel. However, in case of slow-reacting backends you may need to lower (rather than increase) this default by setting `--checkers` to 4 or less threads.  
### Safety and Integrity.  
4. **` Enable checksum to compare files`** :  
   Normally rclone will look at modification time and size of files to see if they are equal. If you set this flag then rclone will check the file hash and size to determine if files are equal.This is very useful when transferring between remotes which store the same hash type on the object, e.g. Drive and Swift. For details of which remotes support which hash type see the table in the [overview section](https://rclone.org/overview/).  

### Error control:  
5. **`Retry the entire sync if it fails this many times`**:  
   Retry the entire sync if it fails this many times it fails (default 3). Some remotes can be unreliable and a few retries help pick up the files which didn't get transferred because of errors. Disable retries with `1`.  

</details>



### Step 3: Filter files and folders (optional)

- RcloneView applies basic filters by default for services like Google Docs or Box Docs.
- You can add more file types or folders to exclude from the sync.

<details>
<summary>Filering Settings Details</summary>

<img src="/support/images/en/howto/rcloneview-basic/sync-filtering-settings-details.png" alt="sync filtering settings details" class="img-medium img-center" />

1. **`Don't sync files over`** :  
   Controls the **maximum file size** allowed for sync.  
   Default unit is MB.  
2. **`Don't sync files older than this`** :    
   Controls the **maximum file age** allowed for sync.  
   This applies to **files only**, not directories.  
   Use the following units:  
   `y` = years, `d` = days, `h` = hours, `m` = minutes, `s` = seconds  (Example: 2y30d12h30m45s)  
3. **`Don't sync folders over this depth`** :   
   If set, Rclone will only sync folders within the specified depth.  
   For example, setting this to `1` will only sync files in the top-level directory.  
   Setting it to `2` will sync files within the first two folder levels, and so on.
4. **Predefined Filters**.   
   You can quickly apply built-in filters for common file types such as:  
   - Music, Video, Image, Document, Google Docs, Box Docs  
     These filters are available as predefined options in the filter list.
1. **Others (= Custom Filters)**.  
   You can define custom rules to exclude or include specific file types, folders, or paths.  
   Here are some common examples:  
   **`.iso`** : Exclude all .iso files.  
   **`/.git/*`** : Exclude only files inside the .git folder in the root, not subfolders.  
   **`/.git/`** :  Exclude the entire .git folder in the root, including everything inside it.   
   **`.git/`** : Exclude all .git folders and everything inside them, regardless of location.   
   
   🔗 For more advanced examples and syntax, refer to the [Rclone Filtering Guide](https://rclone.org/filtering/#exclude-exclude-files-matching-pattern)


</details>

  
  
### Step 4: Run sync

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



## Save sync operation as a Job

If you regularly perform the same sync task, you can save it as a **Job** for easy reuse.

- Click **`Save to Jobs`** after configuring your sync.
- Enter a **Job Name**, then click **Save** to store the job.  
  - ❗Allowed characters: `a–z`, `A–Z`, `0–9`, `-`, `_`, `.`
- You can later run the saved Job from the **`Job Manager`** with one click.

<img src="/support/images/en/howto/rcloneview-basic/save-sync-to-jobs.png" alt="save sync to jobs" class="img-medium img-center" />
You can view and run saved jobs by clicking the **`Job Manager`** toolbar in the Home menu.
<img src="/support/images/en/howto/rcloneview-basic/verify-job-in-job-manager.png" alt="verify job in job manager" class="img-medium img-center" />
