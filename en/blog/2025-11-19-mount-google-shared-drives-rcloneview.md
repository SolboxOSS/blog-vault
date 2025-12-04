---
slug: mount-google-shared-drives-rcloneview
title: "Mount Google Shared Drives in Windows & macOS with RcloneView -- Full Access, No Sync Client Needed"
authors:
  - tayson
description: Mount any Google Shared Drive straight to Finder or File Explorer with RcloneView's guided workflow, bypassing Drive for Desktop limits while keeping admin-level control.
keywords:
  - google shared drive mount
  - mount shared drive windows
  - mount shared drive mac
  - rcloneview
  - rclone mount google drive
  - team drive windows
  - shared drive explorer
  - google workspace shared drive
  - rclone gui
  - mount team drive
tags:
  - RcloneView
  - GoogleDrive
  - Mount
  - Productivity
  - Workspace
---

import RvCta from '../src/components/RvCta';

# Mount Google Shared Drives in Windows & macOS with RcloneView -- Full Access, No Sync Client Needed

> Give every team the Shared Drive they need without forcing a full sync client on their laptops.

Google Workspace Shared Drives often hold your design assets, handover folders, or compliance archives, yet Drive for Desktop only keeps a small cache and struggles with dozens of Shared Drives per user. RcloneView builds on rclone's mature Shared Drive support so you can mount exactly the drive you need as a real drive letter on Windows or a Finder volume on macOS, complete with bandwidth controls, caching, and access logs.

<!-- truncate -->

## Why Teams Need Shared Drive Mounting Without Drive for Desktop

- Drive for Desktop mirrors the whole drive, eating SSD space and leaving laptops offline when quotas are reached.
- Help desks have no way to hand contractors a single Shared Drive without granting account-wide sync rights.
- Engineers and media teams need predictable paths (X:\Marketing or /Volumes/Archive) for automations, scripts, and creative apps.

## How RcloneView Brings Shared Drives to Windows & macOS

RcloneView layers a GUI over rclone, so the Shared Drive picker, auth tokens, and mount flags are handled for you.

- Guided remote wizard lists every Shared Drive that your Google Workspace account can access and stores it securely. See the reference steps in [/support/howto/remote-storage-connection-settings/connect-using-cli/add-google-shared-drive](/support/howto/remote-storage-connection-settings/connect-using-cli/add-google-shared-drive).
- Mount Manager templates the `rclone mount` flags described in [/support/howto/rcloneview-basic/mount-cloud-storage-as-a-local-drive](/support/howto/rcloneview-basic/mount-cloud-storage-as-a-local-drive) so you do not have to memorize CLI syntax.
- Auto-mount, reconnect on boot, and cache location options live under Settings -> General (documented in [/support/howto/rcloneview-basic/general-settings](/support/howto/rcloneview-basic/general-settings)).

## What You Need Before Mounting

| Requirement | Details |
| --- | --- |
| Google Workspace access | Content Manager or higher rights to the Shared Drive you want to mount. Ask admins to confirm API access is enabled. |
| RcloneView + Rclone | Install the latest RcloneView bundle (includes rclone). Confirm `rclone version` >= 1.66 for the newest Drive API fixes. |
| Google API consent | When the Remote wizard opens a browser, sign in with the Workspace account that owns/has access to the Shared Drive. |
| File system drivers | Windows uses WinFsp (bundled). macOS requires macFUSE; follow the prompts inside RcloneView. Check [/support/howto/FAQ/increase-file-handle-limit-on-macos](/support/howto/FAQ/increase-file-handle-limit-on-macos) for tuning limits. |
| Cache space | Allocate a local cache folder (SSD recommended) roughly 2-5% of the dataset for smooth streaming. |

## Step-by-Step: Mount a Google Shared Drive with RcloneView

These steps mirror what admins already do in the CLI but in a friendly wizard so help desks can repeat them quickly.

### Step 1 -- Connect your Google Workspace account

1. Open **Remote Manager** -> **+ New Remote**.
2. Choose **Google Drive** -> **OAuth (Browser)**.
3. After the browser login completes, RcloneView stores the refresh token locally so the Shared Drive stays authorized.

### Step 2 -- Pick the Shared Drive you want

1. When prompted "Configure this as a Shared Drive?", select **Yes**.
2. RcloneView lists all Shared Drives returned by Google. Type the number or search to highlight the correct drive.
3. Save the remote with a descriptive name such as `shared_marketing` so teammates immediately know what it contains.

### Step 3 -- Configure the mount profile

1. Go to **Mount Manager** (or click the mount icon inside Remote Explorer).
2. Select the Shared Drive remote and choose **Mount type -> Google Drive**.
3. Recommended settings:
   - **Mount to system drive letter** (Windows) or **Mount to /Volumes/** (macOS).
   - Enable **Auto mount** so RcloneView reconnects after reboot or sleep.
   - Set **VFS cache mode: full** and choose a cache directory on a fast disk for seamless Office/Adobe editing.
   - Optionally set bandwidth limits or read-only mode for contractors.

### Step 4 -- Launch and verify

1. Click **Save & Mount**. The status chip turns green once the mount is active.
2. In File Explorer or Finder, open the new drive. You should see the Shared Drive folders instantly. Large directories may take a few seconds while RcloneView builds dir cache (default 4 hours).
3. Right-click the mount entry anytime to unmount, edit settings, or open the log file.

## Windows and macOS Quick Commands

RcloneView builds these commands behind the scenes, but it is helpful to understand (and reuse them for scripts).

### Windows: map to a drive letter

1. Choose a free letter such as **X:** in the Mount dialog.
2. RcloneView saves a command similar to:

```powershell
rclone mount shared_marketing: X: --vfs-cache-mode full --cache-dir "D:\\RVCache" --dir-cache-time 4h --poll-interval 15s --transfers 8 --volname "Marketing Shared"
```

3. The drive shows up instantly in Explorer and behaves like a native NTFS volume.

### macOS: mount to Finder

1. Set the mount path to `/Volumes/MarketingShared`.
2. Behind the GUI you get:

```bash
rclone mount shared_marketing: /Volumes/MarketingShared \
  --vfs-cache-mode full \
  --cache-dir "$HOME/Library/Caches/RcloneView" \
  --dir-cache-time 4h \
  --poll-interval 15s \
  --volname "Marketing Shared" \
  --allow-other --umask 002
```

3. The volume appears in Finder's sidebar and supports Spotlight indexing if you enable "Mount as network drive" in preferences.

## Performance & Access Tips

- Keep the cache on SSD and raise the size limit for large media libraries so scrubbing in Premiere, Resolve, or Figma stays fluid.
- Use read-only mounts for finance/legal drives to prevent accidental deletes, and pair them with scheduled sync jobs for backup.
- Set **Dir cache time** to at least one hour for static archives; shorten it (15 minutes) for drives with frequent reorganizations.
- If you script automations, reuse the same mount path so PowerShell, Bash, or Zapier Desktop flows never change.

## Automate, Share, and Secure Access

RcloneView lets you ship standardized mount profiles to every workstation:

- Export/import mount definitions so contractors get the exact same settings (cache, letter, read-only toggle).
- Combine mounts with the **Launch at login** toggle under Settings so the drive is ready before users open Office or Adobe.
- Use the Job Scheduler to mirror Shared Drive content into S3/Wasabi for off-site retention after business hours.
- Surface usage data from the Mount log to monitor throughput and detect throttling before it impacts editors.

## Troubleshooting & FAQ

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Drive disappears after sleep | OS unmounted WinFsp/macFUSE | Enable Auto mount plus "Reconnect on wake" in Settings -> General. |
| Slow file open | Cache too small or USB HDD cache path | Move cache to SSD and allocate >=10 GB; lower `--transfers` for saturated links. |
| Permissions error on macOS | FUSE lacks Full Disk Access | Grant RcloneView and macFUSE Full Disk Access, then restart the mount (Apple menu -> System Settings -> Privacy & Security). |
| `too many open files` | macOS ulimit default 256 | Apply the plist tuning in [/support/howto/FAQ/increase-file-handle-limit-on-macos](/support/howto/FAQ/increase-file-handle-limit-on-macos). |
| Shared Drive list empty | Workspace admin disabled Drive API | Re-enable Drive API in Google Admin or ask for delegated access to the Shared Drive. |

## Ship Shared Drive Mounts Without Scripts

RcloneView makes Shared Drive access predictable: no bloated sync folders, no scripting, and no waiting on IT for each new mount. Give every team a clean drive letter or Finder volume today and keep your Google Workspace storage under control.

<RvCta imageSrc="/img/rcloneview-preview.png" downloadUrl="https://rcloneview.com/src/download.html" />


