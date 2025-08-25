---
sidebar_position: 1
description: Learn how to configure iCloud Drive as a remote in Rclone using the CLI on Windows, including steps for two-factor authentication and integration with RcloneView.
keywords:
  - rcloneview
  - howto
  - cloud
  - sync
  - rclone
  - icloud
  - cli
  - icloud drive
  - rclone cli
  - windows
  - 2fa
  - remote storage
  - cloud storage
  - Remote Connection
  - apple id
tags:
  - cli
  - icloud
  - windows
  - 2fa
  - Remote-Storage
  - remote-connection
  - cloud-storage
date: 2025-05-21
author: Jay
---
# iCloud Drive

The iCloud remote can currently only be added via the Rclone CLI.

:::info
Currently, remotes like iCloud, which support interactive two-factor authentication (2FA), can only be configured via the CLI. Support for configuring these remotes through the UI will be implemented in future releases.
:::

## How to Add iCloud Drive using Rclone CLI (Windows)

#### Step 1: Open Command Prompt

- Press Win + R, type cmd, and press Enter.

<img src="/support/images/en/howto/remote-storage-connection-settings/connect-using-cli/windows-command-prompt.png" alt="windows command prompt" class="img-medium img-left" />

#### Step 2: Start Rclone Configuration

Open the Command Prompt and initiate the Rclone configuration process:

```windows
rclone config
```

You’ll see a menu:

```
No remotes found - make a new one
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
```

Type n and press Enter to create a new remote.

#### Step 3: Set Up the iCloud Drive Remote

Follow the prompts:

- **Name**: Assign a name to your new remote (e.g., icloud).

```windows
Enter name for new remote.
name> Myicloud
```

- **Storage**: Select iCloud Drive by typing `iclouddrive` or its corresponding number (usually `59`) from the list of storage options.If it’s not listed, ensure you’re using Rclone v1.69 or later.

```
Storage> iclouddrive
```

- **Apple ID**: Enter your Apple ID email address.

```
apple_id> your_email@icloud.com
```

- **Password**: Choose to type in your password.

```
y) Yes, type in my own password
g) Generate random password
y/g> y
```

- Enter your Apple ID password when prompted.

```
Enter the password
password:
Confirm the password
password:
```

- **Advanced Config**: Unless you have specific requirements, you can skip advanced configuration.

```
Edit advanced config? (y/n)
y/n> n
```

- **Two-Factor Authentication (2FA)**: If your Apple ID has 2FA enabled (which is recommended), you’ll be prompted to enter the 2FA code sent to your trusted device.

```
Two-factor authentication: please enter your 2FA code
Enter a value.
config_2fa> 123456
```

- **Confirm Configuration**: Review the settings and confirm.

```
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y
```

Your iCloud Drive remote is now configured.

You can verify that the iCloud Drive has been successfully added as shown below. Enter q to exit rclone config.

```
Current remotes:

Name                 Type
====                 ====
Myicloud             iclouddrive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q
```
#### Step 4: Test the connection

To verify that the configuration was successful, list the contents of your iCloud Drive:

```
rclone lsd Myicloud:
```

You should see a list of directories in your iCloud Drive.

#### Step 5: Verify the Added iCloud Drive in RcloneView

Launch **RcloneView**.

1. From the menu bar, click **Remote Manager** under the **Remote** tab.
2. Verify that your **iCloud Drive** appears in the **Remote Manager** window.

<div class="img-grid-2">
<img src="/support/images/en/howto/Remote Storage Connection Settings/Connect using CLI/add-icloud-verify-step1.png" alt="add icloud drive verify step1" class="img-medium img-center" />
<img src="/support/images/en/howto/Remote Storage Connection Settings/Connect using CLI/add-icloud-verify-step2.png" alt="add icloud drive verify step2" class="img-medium img-center" />
</div>

:::danger Important Considerations
- **Advanced Data Protection**: If you have enabled **Advanced Data Protection (ADP)** on your Apple ID, Rclone will not be able to access your iCloud Drive. To use Rclone with iCloud Drive, you must disable ADP. You can do this on your iPhone by navigating to:

```
Settings > [Your Name] > iCloud > Advanced Data Protection
```

- Ensure that ‘Advanced Data Protection’ is turned **off**. Additionally, ‘Access iCloud Data on the Web’ must be **enabled**.

- **Session Validity**: The trust token obtained during configuration is valid for **30 days**. After this period, you’ll need to re-authenticate using:

```
rclone reconnect Myicloud:
```

- **App-Specific Passwords**: Currently, Rclone does **not** support app-specific passwords for iCloud Drive. You must use your regular Apple ID password along with 2FA during setup.

For more detailed information, refer to the official Rclone documentation on [iCloud Drive](https://rclone.org/iclouddrive/).
:::





