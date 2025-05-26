---
sidebar_position: 1
description: This is sample Post for writer
keywords:
  - rcloneview
  - howto
  - cloud
  - sync
  - rclone
  - aws account
  - access key id
  - secret key id
tags:
  - RcloneView
  - howto
  - Cloud
  - Sync
  - aws-account
  - secret-key-id
  - access-key-id
date: 2025-05-26
author: Jay
---
# How to Get Your AWS Access Key and Region for Rclone

Before you can add AWS S3 as a remote in RcloneView, you need your AWS **Access Key ID**, **Secret Access Key**, and **Region** code. This guide will walk you through the steps to generate these securely from your AWS account.

## Step-by-Step: Get Your AWS Access Key ID and Secret Access Key

To connect Rclone to AWS S3, you must create an access key in your AWS account:

1. **Log in** to the [AWS Management Console](https://aws.amazon.com/console).
2. Navigate to **IAM (Identity and Access Management)**.  
   You can search for “IAM” in the AWS service search bar.
3. In the left sidebar, click **Users**, then click your **IAM username**.
4. Go to the **Security credentials** tab.
5. Scroll to the **Access keys** section and click **Create access key**.
6. Choose:  
   `✔ Application running outside AWS`
7. Optionally enter a description (e.g., `RcloneView Access`) to help track the key.
8. Click **Create access key**.
9. On the final screen, copy both:
   - **Access Key ID**
   - **Secret Access Key**

:::important
⚠️ These keys will only be shown **once**. Make sure to **store them securely** (e.g., in a password manager).
:::

## How to Find Your AWS S3 Region

You must also know the AWS **Region** where your S3 bucket is located. This is required when setting up the Rclone remote.

### Option 1: Check via AWS S3 Console

1. Visit the [Amazon S3 Console](https://s3.console.aws.amazon.com/s3/home).
2. Find your bucket in the list.
3. The **Region** column will show the region (e.g., `ap-northeast-2` for Seoul, `us-east-1` for Virginia).

### Option 2: Reference the Official Region List

Refer to this official documentation for all available regions and their codes:

👉 [AWS Region Codes and Endpoints](https://docs.aws.amazon.com/general/latest/gr/s3.html)

:::danger Security Tip
🔒 **Never share or expose your AWS credentials publicly.**  
Rotate keys periodically and delete unused keys via the **IAM Console**.
:::
