---
sidebar_position: "1"
id: Quick-start-guide
title: Quick Start Guide
slug: /intro
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
date: <% tp.date.now("YYYY-MM-DD") %>
author: Jay
---


## Installing RcloneView

Download the installation file from the [RcloneView homepage](https://rcloneview.com/src/download.html). Run the installer and follow the instructions to complete the installation.

When the installation is complete, you will see the following screen, confirming successful installation:

<img src="/support/images/howto/Completed-install.png" alt="Completed-install" class="img-medium img-center" />


## Adding a Remote Storage (Google Drive Example)

Next, we'll demonstrate how to add Google Drive as a remote storage.
Click the '+' button in the right pane of the application window to open the "Add New Remote" dialog.

<img src="/support/images/howto/add-new-remote.png" alt="add new remote" class="img-medium img-center" />

Complete the following steps in the "New Remote" modal:

1. Type "google" in the search bar.
2. Select "Google Drive" from the results.
3. Click "Next".
4. In the "Options" modal, click "Next" without making any changes.

<div class="img-grid-2">
<img src="/support/images/howto/new-remote-step1.png" alt="Add new google remote" class="img-medium img-center" />
<img src="/support/images/howto/add-remote-step2.png" alt="Add google drive option" class="img-medium img-center" />
</div>

:::note
Cloud storage providers supporting Single Sign-On (SSO), such as Google Drive, Dropbox, Google Photos, Microsoft OneDrive, Box, pCloud, Yandex Disk, premiumize.me, put.io, and HiDrive, typically allow you to skip the \"Options\" step, automatically completing the connection after SSO authentication.

However, certain SSO-compatible storages like Zoho WorkDrive, Google Cloud Storage, Citrix ShareFile, \"Google Drive Shared with me,\" and Box for Business require additional configuration in the \"Options\" section. Please refer to the documentation provided [here]([insert documentation link]) for detailed instructions.
:::

5. Provide a name for your remote.
6. Click "Next".
7. Click "Save" to complete adding the remote.

<div class="img-grid-2">
<img src="/support/images/howto/add-remote-step3.png" alt="add google drive step3" class="img-medium img-center" />
<img src="/support/images/howto/add-remote-step4.png" alt="add google drive step4" class="img-medium img-center" />
</div>

:::note
Fields marked with an asterisk (*) are required. You won't be able to save unless all required fields are completed. Please follow the on-screen prompts and fill in all necessary information before clicking "Save".
:::

## Connecting Your Remote Storage (SSO: Single Sign-On)

You will be redirected to the Google SSO login page.
Select an existing Google account from the list.

<img src="/support/images/howto/google-choose-account.png" alt="google choose account" class="img-medium img-center" />

Alternatively, select "Use another account" to log in with a different Google account.

<img src="/support/images/howto/google-choose-another-account.png" alt="google choose another account" class="img-medium img-center" />


Log in using your preferred Google login method (password login example shown below).

<img src="/support/images/howto/google-password-login.png" alt="google password login" class="img-medium img-center" />
:::note
If you are using a login method other than the password-based login shown above, please refer to [this guide](https://support.google.com/accounts/answer/12849458) to complete the login process.
:::


Click "Continue" to complete the connection to your Google Drive.

<img src="/support/images/howto/google-trust-rclone.png" alt="google trust rclone" class="img-medium img-center" />

If you see the following screen, your Google Drive has been successfully connected:
<img src="/support/images/howto/google-login-complete.png" alt="google login complete" class="img-medium img-center" />
You are now ready to manage and synchronize your Google Drive files using RcloneView!



## What's Next?

- Basic File Management with RcloneView
- File Synchronization with RcloneView

## 📎 Related documents

- 👉[Remote Storage Connection Settings](../category/Remote-Storage-Connection-Settings)
- 👉[고급 동기화 팁](app://obsidian.md/guides/advanced-sync)

