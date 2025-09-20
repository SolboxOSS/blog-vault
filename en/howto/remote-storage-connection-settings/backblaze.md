---
sidebar_position: 8
description: Learn how to add Backblaze B2 storage in RcloneView.
keywords:
  - rcloneview
  - rclone
  - backblaze
  - b2
  - remote storage
  - cloud storage
  - Remote Connection
tags:
  - backblaze
  - b2
  - remote-connection
  - Remote-Storage
  - cloud-storage
date: 2025-09-20
author: Jay
---

# Backblaze B2

## How to Add Backblaze B2 Using RcloneView (Windows)

### Step 1: Open the Remote Manager

- Click **`+ New Remote`** from the top menu under **`Remote`**.
- Alternatively, click the **`+`** button in the Explorer pane and select **`New Remote`** to start remote configuration.

<div class="img-grid-2">
<img src="/support/images/en/howto/remote-storage-connection-settings/add-new-remote.png" alt="add new remote" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/add-new-remote-explorer.png" alt="add new remote explorer" class="img-medium img-center" />
</div>

### Step 2: Select Backblaze B2 as the Storage Provider

1. In the **Search Provider** bar, type `b2`.
2. Click on the **Backblaze B2** option that appears.

<img src="/support/images/en/howto/remote-storage-connection-settings/add-backblaze-b2-remote.png" alt="add backblaze b2 remote" class="img-medium img-center" />

You’ll then be taken to the configuration screen for Backblaze B2.

### Step 3: Configure Your Backblaze B2 Remote

In the setup form, provide the following required information:

- **Remote name**: A friendly name for your remote (e.g., `MyB2Master`).
- **account**: Your Backblaze **Application Key ID**.
- **key**: Your Backblaze **Application Key**.

After entering the required values, click **`Add Remote`** to save the connection.
<img src="/support/images/en/howto/remote-storage-connection-settings/remote-configure-backblaze-b2.png" alt="remote configure backblaze b2" class="img-medium img-center" />

:::info Where to get these credentials?

- Log into your [Backblaze B2 account](https://secure.backblaze.com/b2_buckets.htm).
- Go to **App Keys**.
- Create or copy an existing key pair:
  - Use the **Key ID** as the `account`
  - Use the **Application Key** as the `key`
:::


### Step 4: Confirm the Added Remote

Once added, your new Backblaze B2 remote (e.g., `MyB2Master`) will appear in the **Remote Manager** list.

You can now:
- Click **`Open`** to browse the remote.
- Use it in copy/sync/mount operations.
- Manage or delete it anytime.

<img src="/support/images/en/howto/remote-storage-connection-settings/remote-manager-backblaze-view.png" alt="remote manager backblaze view" class="img-medium img-center" />

✅ **Done!** You’ve successfully connected your **Backblaze B2** storage to **RcloneView**.


## 🔗 Additional Resources

- 🔐 Manage your keys: [https://secure.backblaze.com/b2_buckets.htm](https://secure.backblaze.com/b2_buckets.htm)
- 📘 App key docs: [https://www.backblaze.com/b2/docs/application_keys.html](https://www.backblaze.com/b2/docs/application_keys.html)

