---
sidebar_position: 5
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
# How to Connect Cloud Remotes Using Browser Based Login.

RcloneView allows you to easily connect to major cloud providers using **OAuth or browser-based login**. Most these remotes only require a remote name. You can leave the Options tab untouched—just proceed to login via browser.

RcloneView will launch a browser window where you can sign in with your account (Google, Microsoft, Dropbox, etc.). Once authenticated, the remote will be automatically added and ready to use.

## Quick Setup Instructions

1. Open RcloneView and click **`+ New Remote`** from the top menu or the Explorer panel.
2. In the **Provider** tab, choose your cloud service.
3. In the **Options** tab, provide any required fields (if applicable).
4. Proceed to the **Save** step and confirm.
5. A browser window will open for OAuth-based login.
6. After login, the remote is ready to use!

👉 For a example, see: [How to Connect Google Drive](../intro.md#step-2-adding-remote-storage-google-drive-example)

## Supported Cloud Providers & Setup Requirements

| Cloud Provider              | OAuth Login Supported | Required Option(s)                                               |
| --------------------------- | --------------------- | ---------------------------------------------------------------- |
| Google Drive                | ✅ Yes                 | None                                                             |
| Google Drive Shared with Me | ✅ Yes                 | **Advanced Options:**<br />`shared_with_me` = **true**           |
| Google Drive Computers      | ✅ Yes                 | **Advanced Options:**<br />`root_folder_id` = `<your folder ID>` |
| Dropbox                     | ✅ Yes                 | None                                                             |
| Dropbox for Business        | ✅ Yes                 | **Advanced Options:**<br />`dropbox_business` = **true**         |
| Microsoft OneDrive          | ✅ Yes                 | None                                                             |
| Box                         | ✅ Yes                 | None                                                             |
| Box for Business            | ✅ Yes                 | `box_sub_type = enterprise`                                      |
| pCloud                      | ✅ Yes                 | None                                                             |
| Yandex Disk                 | ✅ Yes                 | None                                                             |
| premiumize.me               | ✅ Yes                 | None                                                             |
| put.io                      | ✅ Yes                 | None                                                             |
| Zoho WorkDrive              | ✅ Yes                 | `Region` required                                                |
| Google Cloud Storage        | ✅ Yes                 | `Project Number` required                                        |
| Citrix ShareFile            | ✅ Yes                 | `Root Folder ID` equired                                         |
| HiDrive                     | ✅ Yes                 | None                                                             |

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

