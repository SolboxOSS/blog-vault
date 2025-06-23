---
sidebar_position: 4
description: Learn how to add an SFTP remote in RcloneView
keywords:
  - rcloneview
  - SFTP
  - remote storage
  - SSH
  - Remote Connection
tags:
  - RcloneView
  - sftp
  - Remote-Storage
  - ssh
  - remote-connection
date: 2025-06-23
author: Jay
---
# Add SFTP Remote Storage

## How to Add SFTP using RcloneView

### Step 1: Opening New Remote Configuration Window

- Click **`+ New Remote`** from the top menu under **`Remote`**.
- Alternatively, click the **`+`** button in the Explorer pane and select **`New Remote`** to start remote configuration.

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-new-remote.png" alt="add new remote" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-new-remote-explorer.png" alt="add new remote explorer" class="img-medium img-center" />
</div>

### Step 2: Adding SFTP Remote

#### In the **`Provider`** tab:
1. Type **`sftp`** in the search bar.  
2. Select **`sftp (SSH/SFTP)`** from the list.  

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-sftp-remote-provider.png" alt="add sftp remote provider" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-sftp-remote-options.png" alt="add sftp remote options" class="img-medium img-center" />
</div>
#### In the **`Options`** tab:
3. Enter the **host** (e.g., `myserver.example.com` or `192.168.1.100`)  
4. Enter the **username**  
5. Enter the **port number** (default is `22`)  
6. Enter the **password**  


#### In the **`Name`** tab:
7. Enter a **remote name** (e.g., `MySFTPServer`)  

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-sftp-remote-name.png" alt="add sftp remote name" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-sftp-remote-save.png" alt="add sftp remote save" class="img-medium img-center" />
</div>

#### In the **`Save`** tab:
8. Click **`Save`** to finish setup.

### Step 3: Verify the Added SFTP Remote in RcloneView

1. Go to **`Remote > Remote Manager`**
2. Confirm your newly added **SFTP remote** appears in the list.

✅ **Done!** Your SFTP remote is now successfully configured and ready for use in RcloneView.

