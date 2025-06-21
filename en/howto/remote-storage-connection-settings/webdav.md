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
date: 2025-06-20
author: Jay
---
# Add WebDAV Remote Storage

## How to Add WebDAV using RcloneView

### Step 1: Opening New Remote Configuration Window

- Click **`+ New Remote`** from the top menu under **`Remote`**.
- Alternatively, click the **`+`** button in the Explorer pane and select **`New Remote`** to start remote configuration.

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-new-remote.png" alt="add new remote" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-new-remote-explorer.png" alt="add new remote explorer" class="img-medium img-center" />
</div>

### Step 2: Adding WebDAV Remote

#### In the **`Provider`** tab:
1. Search for **`webdav`**.
2. Select **`WebDAV`** from the list.

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-webdav-remote-provider.png" alt="add webdav remote provider" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-webdav-remote-options.png" alt="add webdav remote options" class="img-medium img-center" />
</div>

#### In the **`Options`** tab:
3. Enter Remote URL
4. Enter your login user name
5. Enter your password

<details>
<summary>Options Details</summary>

Options Details

| Field          | Description                                                                                                                                                                                                                |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `url`          | The remote WebDAV URL (e.g., https://webdav.example.com/)  You can also specify a custom port number (e.g., https://webdav.example.com:5020)                                                                          |
| `vendor`       | (Optional) Leave blank or WebDAV-compatible service provider (e.g., fastmail, nextcloud, owncloud, sharepoint, sharepoint-ntlm, rclone)  See full list: [WebDAV Provider Notes](https://rclone.org/webdav/#provider-notes) |
| `user`         | Your login username                                                                                                                                                                                                     |
| `pass`         | Your login password (masked)                                                                                                                                                                                               |
| `bearer_token` | (Optional) Usually left blank                                                                                                                                                                                              |



</details>
#### In the **`Name`** tab:
6. Enter a unique and identifiable name for this remote (e.g., `myWebDAV`).

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-webdav-remote-name.png" alt="add webdav remote name" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-webdav-remote-save.png" alt="add webdav remote save" class="img-medium img-center" />
</div>
#### In the **`Save`** tab:
5. Click **`Save`** to complete the remote setup.

### Step 3: Verify the Added WebDAV Remote in RcloneView

1. From the top menu, click **`Remote Manager`** under the **`Remote`** tab.
2. Confirm that your **WebDAV remote** appears in the **Remote Manager** window.

✅ **Done!** Your WebDAV remote is now successfully configured and ready to use in RcloneView.