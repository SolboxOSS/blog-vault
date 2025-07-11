---
sidebar_position: 2
description: Learn how to configure cloud remotes in RcloneView using OAuth or browser-based.
keywords:
  - rcloneview
  - SSO
  - OAuth
  - Dropbox
  - Onedrive
  - Box
  - pCloud
  - Yandex
  - premiumize
  - put
  - zoho
  - google cloud storage
  - citrix
  - sharefile
  - hidrive
  - rclone
tags:
  - SSO
  - OAuth
  - dropbox
  - onedrive
  - box
  - pcloud
  - yandex
  - premiumizw
  - PLUS-Feature
  - zoho
  - google-cloud-storage
  - citrix
  - sharefile
  - hidrive
date: 2025-06-23
author: Jay
---
# Auto Login (OneDrive, Box ...)

RcloneView makes it easy to connect to major cloud providers like **Google Drive, OneDrive, Dropbox, Box** using a simple browser-based login (OAuth).

:::important No Options Required
**✅ For most providers, you only need to enter a remote name.**  
**✅ You can skip the Options tab and proceed directly to browser login.**
:::

When you click **Save**, RcloneView will open a browser window where you can sign in to your cloud account. Once you complete the login, your remote will be automatically added and ready to use—no manual setup needed.

## 🚀 Quick Setup Guide

1. Launch **RcloneView** and click **`+ New Remote`** from the top menu or Explorer panel.
2. In the **Provider** tab, select your cloud service (e.g., Google Drive, OneDrive).
3. Skip the **Options** tab (unless prompted for extra info). See the table below for guidance.
4. Go to the **Save** step and click **Save**.
5. A browser window will open — log in to your cloud account.
6. After login, the remote will be added automatically.

👉 Want a detailed example? See: [How to Connect Google Drive](../intro.md#step-2-adding-remote-storage-google-drive-example)

## Supported Cloud Providers & Setup Requirements

| Cloud Provider              | Required Option(s)                                               |
| --------------------------- | ---------------------------------------------------------------- |
| Google Drive                | None                                                             |
| Google Drive Shared with Me | **Advanced Options:**<br />`shared_with_me` = **true**           |
| Google Drive Computers      | **Advanced Options:**<br />`root_folder_id` = `<your folder ID>` |
| Dropbox                     | None                                                             |
| Dropbox for Business        | **Advanced Options:**<br />`dropbox_business` = **true**         |
| Microsoft OneDrive          | None                                                             |
| Box                         | None                                                             |
| Box for Business            | `box_sub_type = enterprise`                                      |
| pCloud                      | None                                                             |
| Yandex Disk                 | None                                                             |
| premiumize.me               | None                                                             |
| put.io                      | None                                                             |
| Zoho WorkDrive              | `Region` required                                                |
| Google Cloud Storage        | `Project Number` required                                        |
| Citrix ShareFile            | `Root Folder ID` equired                                         |
| HiDrive                     | None                                                             |

## Example: Google Drive Shared with Me (requires Advanced Options)

**Google Drive Shared with Me** allows users to access files and folders that other users have explicitly shared with them, without adding them to their own drive. This is useful when collaborating across organizations or teams without duplicating storage.

RcloneView supports this feature through an advanced option setting during remote configuration.

In the **Options** tab:

1. Scroll down and click **`Show advanced options`** at the bottom of the screen.
2. Locate the `shared_with_me` field and set it to **`true`** from the dropdown.
3. Leave other options as default unless custom configuration is required.
4. Click **Next**, then complete the login in your browser when prompted.

:::tip
The `shared_with_me = true` setting instructs Rclone to only show files and folders shared with your Google account.
:::

<img src="/support/images/en/howto/remote-storage-connection-settings/google-drive-shared-with-me-options.png" alt="google drive shared with me options" class="img-medium img-center" />
## Example: Google Drive Computers (requires Advanced Options)

**Google Drive "Computers"** is a feature that syncs local files from your devices (e.g., laptops or desktops) to the cloud under a special "Computers" section in Google Drive. Each computer appears as a separate folder and requires a unique `root_folder_id` to access via Rclone.

🔗 Learn more about this feature: [Access synced computers in Google Drive](https://support.google.com/drive/answer/3096479)

### How to Connect Google Drive Computers in RcloneView

1. Open [drive.google.com](https://drive.google.com/) and click on your target computer (e.g., **My Laptop**) under the **Computers** section.
2. Copy the **Computer ID** from the URL.  
   For example, in  
   `https://drive.google.com/drive/folders/1CxHRI9sdfeeeerAW_1dThrh0W-ze0m2snZ`,  
   the ID is the string after `folders/`:  
   `1CxHRI9sdfeeeerAW_1dThrh0W-ze0m2snZ  
3. Open **RcloneView**, click **`+ New Remote`** under the **Remote** menu, select **Google Drive**, and proceed to the **Options** tab.
4. Scroll down and click **`Show advanced options`**.
5. Paste the copied Computer ID into the `root_folder_id` field.
6. Click **Next** and follow the OAuth login to finish setup.

<div class="img-grid-3">
  <img src="/support/images/en/howto/remote-storage-connection-settings/google-drive-computers-id-copy.png" alt="google drive computers id copy" class="img-medium img-center" />
  <img src="/support/images/en/howto/remote-storage-connection-settings/add-google-drive-computer-remote-options.png" alt="add google drive computer remote options" class="img-medium img-center" />
  <img src="/support/images/en/howto/remote-storage-connection-settings/add-google-drive-computers-options-root-folder-id.png" alt="add google drive computers options root folder id" class="img-medium img-center" />
</div>

✅ After setup is complete, you can browse and access your device-synced Google Drive folders directly within RcloneView.

## Example: Connecting Box for Business

In the **Options** tab:
- Select **enterprise** for `box_sub_type`
- Proceed with default settings  
- When prompted, sign in via your organization’s SSO portal in the browser


✅ Once logged in, the remote will appear in RcloneView and is ready to use.

