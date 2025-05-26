---
sidebar_position: 3
description: How to add SharePoint for Microsoft 365 Business.
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
date: 2025-05-22
author: Jay
---
# Add SharePoint for Microsoft 365 Business Users

## How to Add Sharepoint Using Rclone CLI (Windows)

### Step 1: Open Command Prompt

- Press `Win + R`, type `cmd`, and press `Enter`.

<img src="/support/images/en/howto/remote-storage-connection-settings/connect-using-cli/windows-command-prompt.png" alt="windows command prompt" class="img-medium img-left" />
### Step 2: Start Rclone Configuration

In the Command Prompt window, type:

```windows
rclone config
```

You'll see the following menu:

```
No remotes found - make a new one
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
```

Type `n` and press Enter to create a new remote.

### Step 3: Set Up SharePoint

Follow these prompts:

- **Name**: Give a meaningful name to your remote (e.g., `mySharePoint`).

```windows
Enter name for new remote.
name> mySharePoint
```

- **Storage**: Select OneDrive by typing `onedrive` or its corresponding number (usually `36`) from the list.

```
Storage> onedrive
```

- **client_id and client_secret**: Leave blank unless you have specific credentials.

```
client_id> (press Enter)
client_secret> (press Enter)
```

- **Region**: Choose global by default.

```
Choose national cloud region for OneDrive.
Choose a number from below, or type in your own value of type string.
Press Enter for the default (global).
 1 / Microsoft Cloud Global
   \ (global)
 2 / Microsoft Cloud for US Government
   \ (us)
 3 / Microsoft Cloud Germany (deprecated - try global region first).
   \ (de)
 4 / Azure and Office 365 operated by Vnet Group in China
   \ (cn)
region> (press Enter)
```

- **Option tenant**: Leave empty unless specifically needed.

```
Enter a value. Press Enter to leave empty.
tenant> (press Enter)
```

- **Edit advanced config?** Enter `n`.

```
Edit advanced config? (y/n)
y/n> n
```

- **Use auto config?** Enter `y`.

```
Use web browser to automatically authenticate rclone with remote?
....
y) Yes (default)
n) No
y/n> y
```

A browser window will open automatically. [Log in with your Microsoft account (business account) and grant requested permissions.](../../intro.md#connecting-your-remote-storage-sso-single-sign-on)

### Step 4: Configure SharePoint Site

After authentication, select your account type:

- To add a SharePoint site, select option `2` (Root SharePoint site) or `4` (Search for a SharePoint site):

```
Choose a number from below, or type in an existing value of type string.
Press Enter for the default (onedrive).
 1 / OneDrive Personal or Business
   \ (onedrive)
 2 / Root Sharepoint site
   \ (sharepoint)
   / Sharepoint site name or URL
 3 | E.g. mysite or https://contoso.sharepoint.com/sites/mysite
   \ (url)
 4 / Search for a Sharepoint site
   \ (search)
 5 / Type in driveID (advanced)
   \ (driveid)
 6 / Type in SiteID (advanced)
   \ (siteid)
   / Sharepoint server-relative path (advanced)
 7 | E.g. /teams/hr
   \ (path)
config_type> 2
```

- Enter your SharePoint site URL or select from the search results.

- Review and confirm the displayed configuration:

```
Keep this "mySharePoint" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y
```

- Exit Rclone configuration:

```
Current remotes:

Name                 Type
====                 ====
mySharePoint         onedrive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q
```

**Done!** Your SharePoint site is now successfully configured.

### Step 5: Test the Connection

Verify your configuration by listing the contents of your SharePoint site:

```
rclone ls mySharePoint:
```

If configured correctly, you'll see your files listed.

### Step 6: Verify SharePoint in RcloneView

Launch **RcloneView**.

1. Click **Remote > Remote Manager** from the menu bar.

2. Confirm your **SharePoint** appears in the **Remote Manager** window.

<div class="img-grid-2">
<img src="/support/images/en/howto/Remote Storage Connection Settings/Connect using CLI/add-icloud-verify-step1.png" alt="add icloud drive verify step1" class="img-medium img-center" />
<img src="/support/images/en/howto/remote-storage-connection-settings/connect-using-cli/add-sharepoint-for-ms365.png" alt="add sharepoint for microsoft 365 business" class="img-medium img-center" />
</div>
