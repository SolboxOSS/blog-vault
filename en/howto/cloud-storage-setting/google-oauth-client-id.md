---
sidebar_position: 1
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
date: 2025-06-24
author: Jay
---
# How to Create a Google OAuth Client ID for Rclone (Google Photos)

This guide explains how to create your own OAuth Client ID and use it with Rclone to access Google Photos securely.


## ✅ Step 1: Access Google Cloud Console

- Visit [https://console.cloud.google.com/](https://console.cloud.google.com/)
- Sign in with your Google account.


## ✅ Step 2: Create a New Project

1. Click the **`project dropdown`** at the top of the page.
2. Click **"New Project"**.
3. Enter a name (e.g., `rclone-photos`) and click **Create**.

:::info Location of the Project Dropdown
The label shown in this dropdown may vary depending on your current Google Cloud setup.  
However, you can always find the project selector at the location highlighted in the image below.  
Click the toolbox icon to create a new project.

<img src="/support/images/en/howto/cloud-storage-setting/google-console-new-project.png" alt="Google Console - New Project" class="img-small img-left" />
:::


## ✅ Step 3: Enable Google Photos Library API

1. Click the **`project dropdown`** again and select newly created project (e.g. rclone-photos)
2. Navigate to **APIs & Services > Library** from the left sidebar.
3. Search for **Google Photos Library API**.
4. Click it, then click the **"Enable"** button.

---

## ✅ Step 4: Configure the OAuth Consent Screen

1. Go to **OAuth consent screen** from the left menu.
2. Click **`Get Started`** to configure Google Auth Platform.
3. Fill out the App Information form:
   - App name (e.g. rclone)
   - User support email (e.g. your email address)
1. Choose **External** as the Audience.
2. Fill out the Contact Information. (eg. your email addres)
3. Click **Create** to finish the setup.


---

## ✅ Step 4: Configure the Data Access Scopes

1. In the left sidebar, go to **Data Access**.
2. Click **“Add or remove scopes”** to configure the data access permissions.
3. In the filter box, type `photoslibrary.readonly` to find the scope `.../auth/photoslibrary.readonly`.
4. Check the box next to the matching scope.
5. Click **“Update”** to apply the selected scopes.
6. Finally, click the **“Save”** button to complete the Data Access Scopes configuration.


---

## ✅ Step 5: Create OAuth Client ID

1. Go to **`Clients`** and click **`+Create client`**  to create OAuth client ID
2. Choose **Desktop app** as the application type.
3. Give it a name (e.g., `rclone-desktop`) and click **Create**.
4. Copy or download the **Client ID** and **Client Secret**.



---

## ✅ Step 6: Configure RcloneView to Use the OAuth Credentials

