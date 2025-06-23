---
sidebar_position: "1"
description: Quick start guide to use RcloneView.
keywords:
  - rclone
  - cloud
  - sync
  - rcloneview
  - guide
tags:
  - RcloneView
  - Cloud
  - Sync
date: 2025-05-26
author: Jay
---
# Quick Start Guide

This guide will walk you step-by-step through installing **RcloneView** and adding a **Remote Storage (Google Drive)**.

## **Step 1: Installing RcloneView**

1. Download the installation file from the [**RcloneView homepage**](https://rcloneview.com/).
2. Run the downloaded installer and follow the on-screen instructions to complete the installation.
3. When installation is successful, you will see the following confirmation screen:
<img src="/support/images/howto/Completed-install.png" alt="Completed-install" class="img-medium img-center" />
## **Step 2: Adding Remote Storage (Google Drive Example)**

### **Opening New Remote Configuration Window**

- Click **`+ New Remote`** from the top menu under **`Remote`**.
- Alternatively, click the **`+`** button in the Explorer pane and select **`New Remote`** to start remote configuration.
<img src="/support/images/howto/add-new-remote.png" alt="add new remote" class="img-medium img-center" />
### Adding Google Drive Remote

#### In the **`Provider`** tab:

1. Enter **`google`** in the search bar.
2. Select **`Google Drive`** from the results.
3. Click **`Next`**.
#### In the **`Options`** tab:

4. Usually, you can skip this step by directly clicking **`Next`** unless you have specific configurations.

<div class="img-grid-2">
<img src="/support/images/howto/new-remote-step1.png" alt="Add new google remote" class="img-medium img-center" />
<img src="/support/images/howto/add-remote-step2.png" alt="Add google drive option" class="img-medium img-center" />
</div>

:::tip OAuth-based Cloud Remotes

Most cloud storage providers that support OAuth (web-based login), such as **Google Drive**, **Dropbox**, **Google Photos**, **OneDrive**, **Box**, **pCloud**, **Yandex Disk**, **premiumize.me**, **put.io**, and **HiDrive**, allow you to skip the `Options` step—just name your remote and log in via browser.

However, **some providers require additional configuration** in the `Options` tab before OAuth login:
- **Zoho WorkDrive** – Region selection
- **Google Cloud Storage** – Project Number input
- **Citrix ShareFile** – Root Folder ID input
- **Google Drive Shared with Me** – Enable `shared_with_me`
- **Box for Business** – Select `enterprise` for box_sub_type

👉 See guide: [Connect via Web Browser Login](./remote-storage-connection-settings/add-oath-online-login.md#supported-cloud-providers--setup-requirements)
:::

#### In the **`Name`** tab:

5. Enter a recognizable **`Remote name`** (e.g., MyGoogleDrive).
6. Click **`Next`**.

#### In the **`Save`** tab:

7. Review your settings and click **`Save`** to finish adding the remote.

<div class="img-grid-2">
<img src="/support/images/howto/add-remote-step3.png" alt="add google drive step3" class="img-medium img-center" />
<img src="/support/images/howto/add-remote-step4.png" alt="add google drive step4" class="img-medium img-center" />
</div>

:::tip
Fields marked with an asterisk (*) are required. Ensure all mandatory fields are completed before saving.
:::

## **Step 3: Connecting Your Remote Storage (GoogleDrive Single Sign-On)**
### Account Authentication

- You will be redirected to the Google SSO login page.
- Select your Google account or choose **"Use another account"** to sign in with a different account.

<img src="/support/images/howto/google-choose-account.png" alt="google choose account" class="img-medium img-center" />
:::tip
If you are using a login method other than the password-based login shown above, please refer to [this guide](https://support.google.com/accounts/answer/12849458) to complete the login process.
:::

### Authorize RcloneView Access

- Click "Continue" to complete the connection to your Google Drive.

<img src="/support/images/howto/google-trust-rclone.png" alt="google trust rclone" class="img-medium img-center" />
- You should see a confirmation page displaying **"Success!"**
<img src="/support/images/howto/google-login-complete.png" alt="google login complete" class="img-medium img-center" />
✅ **Done!** Your Google Drive remote is now successfully connected and ready to use in RcloneView.


