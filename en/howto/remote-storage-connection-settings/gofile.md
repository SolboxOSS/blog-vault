---
sidebar_position: 6
description: Learn how to add Gofile storage in RcloneView.
keywords:
  - rcloneview
  - rclone
  - gofile
  - remote storage
  - cloud storage
  - Remote Connection
tags:
  - gofile
  - remote-connection
  - Remote-Storage
  - cloud-storage
date: 2025-05-27
author: Jay
---
# Gofile

## How to Add Gofile Using RcloneView (Windows)


### Step 1: Opening New Remote Configuration Window

- Click **`+ New Remote`** from the top menu under **`Remote`**.
- Alternatively, click the **`+`** button in the Explorer pane and select **`New Remote`** to start remote configuration.

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-new-remote.png" alt="add new remote" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-new-remote-explorer.png" alt="add new remote explorer" class="img-medium img-center" />
</div>
### Step 2: Adding Gofile Remote

#### In the **`Provider`** tab:

1. Search for **`gofile`**.
2. Select **`Gofile`** from the list.

#### In the **`Options`** tab:

3. Enter your **Access Token**.

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-gofile-remote-provider.png" alt="add go file provider" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-gofile-remote-option.png" alt="add gofile remote option" class="img-medium img-center" />
</div>
:::info How to get Access Token
 - Visit [https://gofile.io/myprofile](https://gofile.io/myprofile)
 - Log in to your Gofile account.
- Scroll down to find **`Account API Token`** and copy it.
:::

#### In the **`Name`** tab:

4. Assign a **`Remote name`** to this remote (e.g., `myGofile`).

#### In the **`Save`** tab:

5. Click **`Save`** to finish adding the remote.

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-gofile-remote-name.png" alt="add go file remote name" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-gofile-remote-save.png" alt="add gofile remote save" class="img-medium img-center" />
</div>


### Step 3: Verify the Added Gofile Remote in RcloneView

Launch **RcloneView**.

1. From the menu bar, click **`Remote Manager`** under the **`Remote`** tab.
2. Confirm that your **`Gofile`** remote appears in the **`Remote Manager`** window.

<div class="img-grid-2">
<img src="/support/images/en/howto/Remote Storage Connection Settings/Connect using CLI/add-icloud-verify-step1.png" alt="verify aws s3 step1" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-gofile-remote-verify.png" alt="add go file remote verify" class="img-medium img-center" />
</div>


✅ **Done!** Your **`Gofile`** remote is now successfully configured and ready to use in **RcloneView**.


## 🔗 Additional Resources

- 🔐 Get your token: [https://gofile.io/myprofile](https://gofile.io/myprofile)
