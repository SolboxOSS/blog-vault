---
sidebar_position: 10
description: Learn how to configure general preferences, interface layout, paths, and embedded Rclone settings in RcloneView.
keywords:
  - rcloneview
  - rclone
  - rcloneview settings
  - general preferences
  - dark mode
  - rclone log
  - rclone configurations
tags:
  - RcloneView
  - settings
  - configuration
  - preferences
date: 2025-06-22
author: Jay
---
# General Settings

RcloneView's **Settings** page allows you to configure language, paths, logging options, and interface preferences. This guide explains each section and its functionality.

## General Options

<img src="/support/images/en/howto/rcloneview-basic/general-settings.png" alt="general settings" class="img-medium img-center" />

- **Language**: Select your preferred language for the RcloneView user interface.  

- **Launch at login**: When enabled, RcloneView will automatically start when the user logs into the system.

:::important Auto Start: Scheduling and Mounting

When **Launch at login** is enabled:  

- Any scheduled jobs defined in the [**Job Scheduler**](../rcloneview-advanced/job-scheduling-and-execution.md) will automatically run upon login.  
- Any remotes configured for auto-mounting in the [**Mount Manager**](./mount-cloud-storage-as-a-local-drive.md#method-1-mount-from-remote-explorer) will be mounted automatically when RcloneView starts.  
:::

### Locations
Specify the locations for key components:

- **Local Rclone location**: Path to the `rclone` binary.
- **Local Rclone config location**: Path to `rclone.conf`, where remote definitions are stored.
- **Default download folder**: Folder used for downloads from remote to local.
- **Default upload folder**: Folder used as the source for uploads to remote.

:::caution Restart rclone Required to Apply Location Changes

Click **`Restart rclone`** to apply any changes made to the location settings.  
This will restart the embedded Rclone instance and may interrupt any currently running jobs.  

:::

## Interface Preferences

<img src="/support/images/en/howto/rcloneview-basic/interface-settings.png" alt="interface settings" class="img-medium img-center" />
Customize how the interface behaves:

- **Dark mode**: Enable dark theme.
- **Theme color**: Choose from predefined accent colors.
- **Confirm drag and drop**: Prompts confirmation when dragging files.
- **Jobs view items**: Show or hide job types: Download, Upload, Sync.
- **Show job state log**: Notify dialog to displays logs for each job execution.
- **Show comparison completed**: Alerts dialog when folder comparison finishes.
- **Show confirmation dialog before deleting files in compare**: Confirm dialog to add extra safety before deletion.
- **Show sync completion notification**: Notify dialog when sync job completes.
- **Show network error dialog**: Alert dialog for network failures.

## Embedded Rclone Configuration

<img src="/support/images/en/howto/rcloneview-basic/embedded-rclone-settings.png" alt="embedded rclone settings" class="img-medium img-center" />
- **Stop embedded rclone with RcloneView**: Terminates the rclone process when RcloneView closes.
- **Enable embedded rclone log**: Enables logging for embedded rclone operations.
	Logging options:  
	- **Log folder**: Path where log files are saved.  
	- **Log file name**: Customize the filename for rclone logs.  
	- **Log level**: Choose from standard rclone log levels (DEBUG, INFO, NOTICE, ERROR).  

Advanced options:  
- **Rclone global flags**: Enter any global rclone flags (e.g. `--no-check-certificate`).  
- **Rclone config password**: Password for encrypted rclone configurations. If you set this password, then rclone config files will be encrypted.  

:::caution Restart rclone Required to Apply Embedded Rclone Settings

Click **`Restart rclone`** to apply any changes made to the Embedded Rclone settings.  
This will restart the embedded Rclone instance and may interrupt any currently running jobs.  

:::

## Network & Logs

<img src="/support/images/en/howto/rcloneview-basic/network-etc-settings.png" alt="network etc settings" class="img-medium img-center" />
### Network
- **`Proxy settings`**: Features coming soon.
- **`Rclone connection manager`**: Open [**Connection Manager**](./connection-manager.md)

### Etc
- **`Application Log`**: Open log viewer for app-level logs.

- **`Restore Settings`**: Reset all settings to default values.

---
