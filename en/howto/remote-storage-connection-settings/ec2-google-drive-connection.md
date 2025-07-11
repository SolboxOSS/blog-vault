---
sidebar_position: 7
description: Learn how to add a Google Drive remote to an external Rclone running on AWS EC2 without using a web browser, using OAuth tokens generated locally.
keywords:
  - rcloneview
  - rclone
  - google drive
  - OAuth
  - token
  - ec2
  - external rclone
  - no browser login
  - headless
  - cloud storage
  - Remote Connection
  - remote storage
tags:
  - Remote-Storage
  - google-drive
  - external-rclone
  - aws-ec2
  - remote-connection
  - cloud-storage
date: 2025-07-07
author: Jay
---
# Google Drive to External Rclone on AWS EC2 (Without Web Browser)

This guide explains how to add a **Google Drive remote** to an **external Rclone instance** running on a system where a web browser is not available—such as an **AWS EC2 Ubuntu server**.

In such environments, completing the standard OAuth login flow via browser is not possible. Instead, you can use a local RcloneView installation to obtain the required **OAuth token**, and then reuse it on the external Rclone running on EC2.

:::info Run Rclone Daemon on EC2
For instructions on how to install and run Rclone on an EC2 instance, 

see: 👉 [How to Run Rclone Engine on AWS EC2](../cloud-storage-setting/run-rclone-on-aws-ec2.md)

:::

The process involves performing an OAuth login on your **local RcloneView** using the embedded Rclone engine, then copying the resulting OAuth token and using it to configure the remote on the external EC2-based Rclone.

---

## ✅ Step 1: Connect Google Drive via Embedded Rclone (with Browser OAuth)

Follow this guide on your **local machine with browser access** to set up Google Drive using the embedded Rclone:  
👉 [Quick Guide: Add Google Drive Remote](../intro.md#step-2-adding-remote-storage-google-drive-example)

Once added successfully, you will be able to retrieve the required OAuth token.

---

## ✅ Step 2: Copy the OAuth Access Token

1. In **`Remote Manager`**, locate the connected Google Drive remote.
2. Click **`Edit`** to open its settings.
3. In the **`Options`** tab, scroll down and click **`Show advanced options`**.
4. Copy the content of the **`Token`** field. This contains the OAuth credentials that will be reused on the external Rclone.

<img src="/support/images/en/howto/remote-storage-connection-settings/copy-google-oauth-token-from-embedded-rclone.png" alt="copy google oauth token from embedded rclone" class="img-medium img-center" />

👉 Learn more: [Edit Remote Settings](../rcloneview-basic/remote-manager.md#edit-remote-settings)

---

## ✅ Step 3: Connect to the External Rclone (EC2)

Open a **`new window`** or use your current session in RcloneView to connect to your EC2-hosted Rclone:

- Open `Settings` → **`Connection Manager`** to either create a new connection to your EC2-hosted Rclone or connect to an existing one if already configured.

👉 Learn more: [Connect External Rclone](../rcloneview-basic/connection-manager.md#add-a-new-external-rclone)  
👉 Learn more: [New Window Feature](../rcloneview-advanced/multi-window.md#new-window-feature-managing-both-models)

---

## ✅ Step 4: Add Google Drive Remote to the External Rclone

1. In the EC2-connected window, go to the `Remote` menu and select **`+ New Remote`**.
2. Choose **Google Drive** as the provider.
3. In the **`Options`** tab, scroll to the bottom and click **`Show advanced options`**.
4. Paste the previously copied **OAuth Token** into the **`Token`** field.
5. Complete the setup as usual.

<img src="/support/images/en/howto/remote-storage-connection-settings/copy-google-oauth-token-to-external-rclone.png" alt="copy google oauth token to external rclone" class="img-medium img-center" />

Once configured, your EC2-based Rclone can now access Google Drive even without browser support. You can manage, sync, and transfer files using RcloneView as usual.

---

## 🔗 Related Guides

- [How to Run Rclone Engine on AWS EC2](../cloud-storage-setting/run-rclone-on-aws-ec2.md)
- [Add Google Drive Remote](../intro.md#step-2-adding-remote-storage-google-drive-example)
- [Edit Remote Settings](../rcloneview-basic/remote-manager.md#edit-remote-settings)
- [Connect External Rclone](../rcloneview-basic/connection-manager.md#add-a-new-external-rclone)
- [Multi-Window Usage](../rcloneview-advanced/multi-window.md#new-window-feature-managing-both-models)

