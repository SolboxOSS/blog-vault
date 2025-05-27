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

:::note
Cloud storage providers supporting Single Sign-On (SSO), such as Google Drive, Dropbox, Google Photos, Microsoft OneDrive, Box, pCloud, Yandex Disk, premiumize.me, put.io, and HiDrive, typically allow you to skip the \"Options\" step, automatically completing the connection after SSO authentication.
:::
:::tip
However, certain SSO-compatible storages like Zoho WorkDrive, Google Cloud Storage, Citrix ShareFile, \"Google Drive Shared with me,\" and Box for Business require additional configuration in the \"Options\" section. Please refer to the documentation provided [here]([insert documentation link]) for detailed instructions.
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

:::note
Fields marked with an asterisk (*) are required. Ensure all mandatory fields are completed before saving.
:::

## **Step 3: Connecting Your Remote Storage (GoogleDrive Single Sign-On)**
### Account Authentication

- You will be redirected to the Google SSO login page.
- Select your Google account or choose **"Use another account"** to sign in with a different account.

<img src="/support/images/howto/google-choose-account.png" alt="google choose account" class="img-medium img-center" />
:::note
If you are using a login method other than the password-based login shown above, please refer to [this guide](https://support.google.com/accounts/answer/12849458) to complete the login process.
:::

### Authorize RcloneView Access

- Click "Continue" to complete the connection to your Google Drive.

<img src="/support/images/howto/google-trust-rclone.png" alt="google trust rclone" class="img-medium img-center" />
- You should see a confirmation page displaying **"Success!"**
<img src="/support/images/howto/google-login-complete.png" alt="google login complete" class="img-medium img-center" />
✅ **Done!** Your Google Drive remote is now successfully connected and ready to use in RcloneView.


## 📎 Related documents

- 👉[Add AWS S3](remote-storage-connection-settings/s3.md)
- 👉[Add iCloud Drive](remote-storage-connection-settings/connect-using-cli/add-icloud-drive.md)


