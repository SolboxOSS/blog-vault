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
tags:
  - RcloneView
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
# How to Connect Cloud Remotes Using OAuth or Online Login

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

| Cloud Provider              | OAuth Login Supported | Required Option(s)                                     |
| --------------------------- | --------------------- | ------------------------------------------------------ |
| Google Drive                | ✅ Yes                 | None                                                   |
| Google Drive Shared with Me | ✅ Yes                 | **Advanced Options:**<br />`shared_with_me` = **true**   |
| Dropbox                     | ✅ Yes                 | None                                                   |
| Dropbox for Business        | ✅ Yes                 | **Advanced Options:**<br />`dropbox_business` = **true** |
| Microsoft OneDrive          | ✅ Yes                 | None                                                   |
| Box                         | ✅ Yes                 | None                                                   |
| Box for Business            | ✅ Yes                 | `box_sub_type = enterprise`                            |
| pCloud                      | ✅ Yes                 | None                                                   |
| Yandex Disk                 | ✅ Yes                 | None                                                   |
| premiumize.me               | ✅ Yes                 | None                                                   |
| put.io                      | ✅ Yes                 | None                                                   |
| Zoho WorkDrive              | ✅ Yes                 | `Region` required                                      |
| Google Cloud Storage        | ✅ Yes                 | `Project Number` required                              |
| Citrix ShareFile            | ✅ Yes                 | `Root Folder ID` equired                               |
| HiDrive                     | ✅ Yes                 | None                                                   |

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
## Example: Connecting Box for Business

In the **Options** tab:
- Select **enterprise** for `box_sub_type`
- Proceed with default settings  
- When prompted, sign in via your organization’s SSO portal in the browser


✅ Once logged in, the remote will appear in RcloneView and is ready to use.

