---
sidebar_position: 3
description: How to Obtain Cloudflare R2 Credentials and Endpoint
keywords:
  - rcloneview
  - cloud
  - rclone
  - cloudflare r2
  - r2 endpoint
  - access key id
  - secret access key
  - cloudflare r2 rclone
  - cloudflare s3 api
  - connect r2 to rcloneview
tags:
  - RcloneView
  - Cloud
  - cloud-storage
  - cloudflare
  - credentials
  - configuration
  - access-key-id
  - secret-access-key
  - secret-key-id
date: 2025-07-12
author: Jay
---
# How to Obtain Cloudflare R2 Credentials and Endpoint

To connect **Cloudflare R2** to Rclone or **RcloneView**, you’ll need three key pieces of information:

- ✅ Access Key ID  
- ✅ Secret Access Key  
- ✅ R2 S3-Compatible Endpoint URL  

This guide walks you through how to retrieve these from your Cloudflare dashboard.

---

## 🧰 Prerequisites

Before you begin:

- You must have a Cloudflare account with **R2 Object Storage** enabled.
- You need access to the [Cloudflare Dashboard](https://dash.cloudflare.com).
- Basic understanding of cloud storage concepts is helpful.

---

## 📦 Step 1: Create an R2 Bucket (If You Haven’t Already)

1. Log in to your [Cloudflare Dashboard](https://dash.cloudflare.com).
2. In the left sidebar, go to **R2 → Object Storage**.
3. Click **Create bucket**.
4. Enter a unique name for your bucket.
5. Choose a location (e.g., **Automatic**, or a region like `westerneurope`).
6. Click **Create Bucket**.

This bucket will be your storage location for files transferred using RcloneView.

---

## 🔐 Step 2: Generate API Credentials

To authenticate with R2, you’ll need to create API tokens that provide access permissions.

### ➕ How to Create an Access Key and Secret Key:

1. Go to **R2 → API** in the Cloudflare dashboard.
2. Click **Manage R2 API Tokens**.
   <img src="/support/images/en/howto/cloud-storage-setting/cloudflare-manage-r2-api-token.png" alt="cloudflare manage r2 api token" class="img-medium img-center" />
3. Click **Create API Token**.
4. Give the token a name (e.g., `Rclone Access`).
5. Select the permissions:
   - `Admin Read & Write` (full access)  
   - `Object Read & Write` (typical for file transfers)  
   - `Object Read` (read-only)
6. Choose whether to apply to:
   - All buckets
   - Specific buckets only
7. Optionally, set expiration (or leave as "Forever").
8. Click **Create API Token**.

Once the token is created, Cloudflare will show you:

- **Access Key ID**
- **Secret Access Key**

:::danger Important
These credentials will be shown only once. Make sure to copy and store them securely.
:::

---

## 🌐 Step 3: Get the R2 Endpoint URL

1. Return to **R2 → Object Storage** in your dashboard.
2. Click your **bucket name**.
3. Go to the **Settings** tab of the bucket.
4. Look for the **S3 API-compatible endpoint**. It will look something like this:

```
https://<ACCOUNT_ID>.r2.cloudflarestorage.com/westerneurope
```

<img src="/support/images/en/howto/cloud-storage-setting/cloudflare-r2-s3-api-endpoint.png" alt="cloudflare r2 s3 api endpoint" class="img-medium img-center" />

This is the endpoint you’ll enter into Rclone or RcloneView when connecting to Cloudflare R2.

---
   
## ✅ Summary

You should now have the following values ready to configure your Cloudflare R2 remote:

| Field             | Description                                      |
|------------------|--------------------------------------------------|
| Access Key ID     | Provided by Cloudflare API token                |
| Secret Access Key | Provided by Cloudflare API token                |
| Endpoint URL      | Found in R2 bucket settings (S3-compatible URL) |

You can now enter these into **RcloneView** when setting up a new S3-compatible remote, or use the Rclone CLI.

👉 Next: [How to Add S3-Compatible Remote in RcloneView](/support/howto/remote-storage-connection-settings/s3)
