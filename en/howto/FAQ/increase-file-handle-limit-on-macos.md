---
sidebar_position: 1
description: Learn how to resolve "Too many open files" errors on macOS by increasing the file handle limit for smoother operation of RcloneView.
keywords:
  - rcloneview
  - macos
  - file handle limit
  - rclone
  - plist
  - ulimit
tags:
  - RcloneView
  - macOS
  - Troubleshooting
  - FAQ
  - Performance
  - system-settings
date: 2025-07-25
author: Jay
---
# Increasing File Handle Limit on macOS

When using RcloneView to process a large number of files (e.g., syncing or copying hundreds of files simultaneously), you may encounter the following error:

> **Too many open files**

This occurs because macOS imposes a limit on the number of file descriptors (file handles) a process can open. By default, this value is often set to **256 or 1024**, which may be insufficient for heavy operations.

---

## 🔍 How to Check Current Limits

### Terminal Command:

```bash
ulimit -n             # Current shell session soft limit
launchctl limit maxfiles  # System-wide soft and hard limits
```

---

## 🛠️ Recommended Configuration

- **Soft Limit:** 65536
- **Hard Limit:** 65536

This configuration supports parallel jobs, mounting remotes, and large sync operations without hitting file descriptor limits.

---

## 📘 Step-by-Step: Permanent Limit Increase

### 1. Create a LaunchDaemon plist file

Open Terminal and run:

```bash
sudo nano /Library/LaunchDaemons/limit.maxfiles.plist
```

Paste the following content:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
   <key>Label</key>
   <string>limit.maxfiles</string>
   <key>ProgramArguments</key>
   <array>
       <string>launchctl</string>
       <string>limit</string>
       <string>maxfiles</string>
       <string>65536</string>
       <string>65536</string>
   </array>
   <key>RunAtLoad</key>
   <true/>
</dict>
</plist>
```

### 2. Set proper permissions

```bash
sudo chmod 644 /Library/LaunchDaemons/limit.maxfiles.plist
```

### 3. Reboot your Mac

```bash
sudo reboot
```

### 4. Confirm the new limits

```bash
launchctl limit maxfiles
```

---
## 📎 Reference Resources

- Apple Support Community: [Too many open files](https://discussions.apple.com/thread/1449787)
- Example Gist: [limit.maxfiles.plist configuration](https://gist.github.com/tombigel/d503800a282fcadbee14b537735d202c)
- Blog Guide: [Hiltmon - Increasing file descriptor ulimit on macOS](https://hiltmon.com/blog/2023/01/01/increasing-file-descriptor-ulimit-on-macos/)

---

For any issues, contact support at **[rcloneview@bdrive.com](mailto:rcloneview@bdrive.com)**.


