---
sidebar_position: 11
description: Learn how to use the Job Monitor in RcloneView to track sync, copy, and delete operations with real-time progress and API logs.
keywords:
  - rcloneview
  - Job Monitor
  - Transfer Log
  - Rclone API Logs
  - file transfer
tags:
  - RcloneView
  - Job-Management
  - Monitoring
  - Transfer-log
  - Completed-log
  - API-log
date: 2025-06-22
author: Jay
---
# Job Monitor

RcloneView provides a **Job Monitor** interface to help users track, review, and manage the status of ongoing and completed file operations such as Sync, Copy, and Delete. The interface consists of three main tabs:

## Transfer Tab - Ongoing Jobs

<img src="/support/images/en/howto/rcloneview-basic/transfer-log.png" alt="transfer log" class="img-medium img-center" />
This tab shows all currently active file transfer jobs.

**Columns:**
- **Job**: Indicates the operation type (e.g., Sync, Copy, Delete).
- **Source / Destination**: Displays the origin and target path.
- **Received Size**: Amount of data transferred / total size.
- **Speed**: Current transfer speed.
- **Progress**: Visual progress bar of the current job.
- **Percentage**: Transfer completion percentage.
- **Time Left**: Estimated remaining time.
- **Job ID**: Internal ID used to reference this job.
- **Cancel**: Click the ❌ icon to cancel the job in progress.

## Completed Tab - Job History

<img src="/support/images/en/howto/rcloneview-basic/completed-log.png" alt="completed log" class="img-medium img-center" />
This tab lists all previously executed jobs and their results.

**Columns:**
- **Job**: The operation type (Sync, Copy, Delete, etc.).
- **Source / Destination**: Path of the source and destination.
- **Status**: Result status (e.g., Success, Errors).
- **Started At**: Start time of the job.
- **Time Spent**: Total duration of the job.
- **Files**: Number of files transferred.
- **Size**: Total data size.
- **Speed**: Average transfer speed.
- **Job ID**: Internal job reference.
- **Delete**: <img src="/support/icons/delete-files.png" alt="delete files" class="inline-icon" /> icon to remove the record.

## Log Tab - API Communication Logs

<img src="/support/images/en/howto/rcloneview-basic/log-tab.png" alt="log tab" class="img-medium img-center" />

This tab displays backend logs from RcloneView's communication with the Rclone API.

**Columns:**
- **Time**: Timestamp of the operation request.
- **Event Type**: Log level (e.g., INFO, ERROR).
- **Job Type**: The operation type (Sync, Copy, Delete, etc.).
- **Message**: Result of the operation.
- **Details**: Additional internal metadata (e.g., job ID in JSON).

Use this tab for troubleshooting or reviewing system-level interactions.

:::tip
- Each job record is linked across the tabs by its **Job ID**.
- Logs are automatically updated in real-time.
- The Completed and Log tabs retain history even after application restarts unless manually deleted.
:::
