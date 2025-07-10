---
sidebar_position: 3
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
date: 2025-07-07
author: Jay
---
# Set Up Rclone with Google Drive on AWS EC2 Ubuntu (Headless Mode)

This guide walks you through configuring Google Drive in rclone on an EC2 instance using **headless (manual) authentication** only via the command line.

---

### Step 1: Connect to Your EC2 Instance via SSH

Follow the guide below to access your EC2 Ubuntu instance:

📄 [Run Rclone on AWS EC2 – SSH into the EC2 Instance](/support/howto/cloud-storage-setting/run-rclone-on-aws-ec2#ssh-into-the-ec2-instance)

---

### Step 2: Configure Rclone for Google Drive

Once connected via SSH and `rclone` is installed:

```bash
rclone config
```

This launches the interactive setup. Follow these steps:

---

#### 🆕 Create a New Remote

```
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
```

- **Name** your remote:  
    → For example: `MyGdrive`
    
---

#### 🌐 Choose Cloud Provider

Select **Google Drive** from the list. It is usually option `22`, but the number may vary.

```
Type of storage to configure.
Choose a number from below, or type in your own value
...
22 / Google Drive
...
Storage> 22
```

---
#### 🔓 Use Default Credentials

You’ll now be asked:

```
Google Application Client Id
Leave blank normally.
client_id>
```

→ Just **press Enter** to use rclone's default.

```
Google Application Client Secret
Leave blank normally.
client_secret>
```

→ Again, **press Enter**.

---

#### 🔍 Choose Scope of Access

You’ll be prompted to select the access level:

```
Scope that rclone should use when requesting access from drive.
Enter a number:
 1 / Full access all files, including documents and photos.
 2 / Read-only access to file metadata and file contents.
...
scope> 1
```

→ Choose `1` for **full access** (recommended for syncing/backups).

---

Option service_account_file.

Service Account Credentials JSON file path.

Leave blank normally.

Needed only if you want use SA instead of interactive login.

Leading `~` will be expanded in the file name as will environment variables such as `${RCLONE_CONFIG_DIR}`.

Enter a value. Press Enter to leave empty.

service_account_file>



Edit advanced config?

y) Yes

n) No (default)

y/n>n



#### 🔒 Manual (Headless) Authentication

Next:

```
Use auto config?
 * Say Y if you are on a machine with a web browser
 * Say N if you are on a remote or headless machine
y/n> 
```

👉 Type `n` and press **Enter**

You’ll then see output like:

```
Please go to the following link: https://accounts.google.com/o/oauth2/auth?client_id=...
Log in and authorize rclone for access
Enter verification code> 
```

---

### 🌐 Step 3: Authorize on Your Local PC

1. **Copy the URL** from the EC2 terminal
    
2. Open it in your **local PC browser**
    
3. Log in to your Google account
    
4. Allow rclone to access your Google Drive
    
5. You’ll get a **verification code**
    
6. Paste that code back into the EC2 terminal
    

---

### ✅ Step 4: Confirm and Save

You’ll now be asked:

```
Configure this as a team drive?
y) Yes
n) No
```

→ Type `n` unless you’re using a Google Workspace Team Drive.

Then:

- You’ll see: `Remote config 'gdrive' saved successfully`
    
- Type `q` to quit the config menu.
    

---

### 🧪 Step 5: Test the Connection

Run this command:

```bash
rclone lsd gdrive:
```

You should see a list of top-level folders in your Google Drive.

---

Let me know if you’d like help using `rclone sync`, `mount`, or `copy` commands next!