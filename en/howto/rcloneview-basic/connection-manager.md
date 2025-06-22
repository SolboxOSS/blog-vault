---
sidebar_position: 9
description: Learn how to manage Embedded and External Rclone instances in RcloneView.
keywords:
  - rcloneview
  - connection
  - remote control
  - embedded rclone
  - external rclone
  - connection manager
tags:
  - RcloneView
  - connection
  - remote-control
  - embedded-rclone
  - external-rclone
  - connection-manager
date: 2025-06-22
author: Jay
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Manage Rclone Connections in RcloneView

RcloneView is a GUI-based file manager for cloud storage that communicates with **Rclone** via its Remote Control (RC) API. By default, it comes bundled with an **Embedded Rclone** instance but also supports connecting to external Rclone instances (**External Rclone**).

This guide explains how to manage these connections using the **Connection Manager**.

## Connection Manager Overview

RcloneView communicates with Rclone in two modes:

- **Embedded Rclone** (default, built-in)
- **External Rclone** (user-configured, network-connected)

The **Connection Manager** allows you to view, switch, and manage these Rclone instances.

<img src="/support/images/en/howto/rcloneview-basic/connection-manager-with-embedded-rclone-only.png" alt="connection manager with embedded rclone only" class="img-medium img-center" />

### Embedded Rclone

RcloneView includes a pre-installed Rclone binary called **Embedded Rclone**, which launches automatically.

| Field                       | Description                                                                    |
| --------------------------- | ------------------------------------------------------------------------------ |
| **Address**                 | Typically `http://127.0.0.1:5582` (localhost loopback)                         |
| **Rclone Version**          | Example: `v1.70.1`                                                             |
| **Connected** / **Connect** | Indicates the current status. If not connected, click **Connect** to activate. |
| **Self Update**             | Click to upgrade to the latest Rclone version.                                 |

### External Rclone List

External Rclone refers to a standalone Rclone instance launched manually by the user, typically via `rclone rcd`. It could be running on:

- A local machine (for testing)
- A remote server (e.g., AWS EC2)
- Inside a Docker container

Each entry displays:

| Field | Description |
|-------|-------------|
| **Display Name** | User-defined name (e.g., `aws-rclone`) |
| **Remote Address** | API endpoint, e.g., `http://<host>:5572` |
| **Username** | If authentication is enabled |
| **Rclone Version** | Retrieved from the connected instance |

**Available Actions**:
- **Connect** – Makes this instance active
- **Edit** – Modify address, credentials, or SSL options
- **Delete** – Remove from the list

<div class="img-grid-2">
<img src="/support/images/en/howto/rcloneview-basic/external-rclone-added.png" alt="external rclone added" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/external-rclone-selected.png" alt="external rclone selected" class="img-medium img-center" />
</div>

### Current Selection Indicator

At the top of the Connection Manager dialog:

- `Selected: Embedded Rclone` – the default built-in instance is active  
- `Selected: aws-rclone` – a custom external instance is in use

Only one connection can be active at a time. Your current selection affects:

- Remote list visibility  
- Mount/Job actions  
- Configuration operations

:::important Notes
- Only one Rclone connection can be active at any time.  
- You can switch freely between Embedded and External connections.  

💡 To manage two instances side-by-side, open a new RcloneView window.

- If an external Rclone becomes unavailable, you can always fall back to the embedded version.
:::

## Add a New External Rclone

To connect to a running `rclone rcd` server:

<img src="/support/images/en/howto/rcloneview-basic/new-connection-form.png" alt="new connection form" class="img-medium img-center" />

1. Click **New Connection** at the bottom of the Connection Manager.
2. Fill in the form:

| Field | Description |
|-------|-------------|
| **Display Name** | e.g., `aws-rclone` |
| **Remote Address** | Full API endpoint (`http://<host>:5572`) |
| **Username / Password** | Required if authentication is enabled |
| **Disable SSL Verification** | For self-signed certificates or dev use |
<br />
<br />

3. Click **Test connection**. If successful, click **Save**.

:::important Notes

💡 To make an external Rclone available, run it with:

```bash
rclone rcd --rc-user=<user> --rc-pass=<pass> --rc-addr=127.0.0.1:5572
```

:::
