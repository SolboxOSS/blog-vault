---
sidebar_position: 2
description: Step-by-step guide to set up and run the Rclone Remote Control (rcd) daemon on an Ubuntu-based AWS EC2 instance, including API access and systemd service configuration.
keywords:
  - rcloneview
  - rclone
  - aws
  - ec2
  - remote control
  - rclone rcd
  - systemd
  - ubuntu
  - daemon
  - cloud storage
  - rclone api
  - external rclone
tags:
  - RcloneView
  - aws
  - aws-ec2
  - remote-server
  - rclone-rcd
  - external-rclone
  - rclone
date: 2025-07-03
author: Jay
---
# Run Rclone Engine on AWS EC2

  This guide walks through setting up **Rclone’s rcd daemon** on an **Ubuntu-based EC2 instance**, enabling remote API access from outside AWS.

---

## **✅ Step-by-Step Overview**

1. [Launch an EC2 instance](#launch-an-ec2-instance)
2. [Configure Security Group (open port 5572)](#adjust-security-group-if-needed)
3. [SSH into the instance](#ssh-into-the-ec2-instance)
4. [Install Rclone](#install-rclone)
5. [Run rclone rcd daemon](#run-the-rclone-rcd-daemon)
6. [Test Rclone API access externally](#verify-external-api-access)
7. [Run Rclone rcd as a systemd Service](#run-rclone-rcd-as-a-systemd-service)

---

### Launch an EC2 Instance

- Log in to the AWS Management Console  
- Navigate to **EC2 → Launch Instance**  
- Configure as follows:  
    - **Name**: rclone-server (or your choice)  
    - **AMI**: Ubuntu Server 22.04 LTS (or 20.04 LTS)   
    - **Instance type**: t2.micro (Free Tier eligible)  
    - **Key pair**: Create a new one or select existing (for SSH access)  
    - **Storage**: At least 8 GB  
    - **Network**: Default VPC  
    - **Security group inbound rules**:  
        - SSH (port 22): restricted to your IP  
        - **Custom TCP (port 5572): 0.0.0.0/0** — required for Rclone API  
- Launch the instance  

---

### Adjust Security Group (if needed)

Visit EC2 → Instances → Select your instance → Security tab → Click Security Group → Edit inbound rules:

```
Type: Custom TCP
Port: 5572
Source: 0.0.0.0/0  (or restrict to your IP)
```

---

### SSH Into the EC2 Instance

From your local terminal:

```
chmod 400 /path/to/your-key.pem
ssh -i /path/to/your-key.pem ubuntu@<EC2-PUBLIC-IP>
```

🔗 For guidance on creating and using .pem key pairs, see [AWS’s official “Create a key pair” page](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html)  .

---

### Install Rclone

```
curl https://rclone.org/install.sh | sudo bash
rclone version
```

---

### Run the rclone rcd Daemon

```
rclone rcd \
  --rc-user=admin \
  --rc-pass=admin \
  --rc-addr=0.0.0.0:5572
```

- --rc-user/--rc-pass: secures API access
- --rc-addr: listens on all interfaces so you can connect externally
- --rc-web-gui: launches the web interface

💡 For continuous operation, consider running it under tmux, screen, or as a systemd service.

---

### Verify External API Access

Run a simple health check using curl:

```
curl -X POST -u admin:admin \
  "http://<EC2-PUBLIC-IP-or-DNS>:5572/rc/noop"
```

Expected response:

```
{}
```

This confirms that the Rclone remote control (RC) API is running and accepting authenticated requests.

:::important 🛠️ Notes
- Be sure to replace admin:admin with the actual --rc-user and --rc-pass you defined when starting the daemon.
- Replace `<EC2-PUBLIC-IP-or-DNS>` with your actual public IP or DNS name of the EC2 instance.
- The endpoint must begin with /rc/. The /rc/noop command does nothing and simply confirms that the API is available.
:::

---

#### **🔐 Recommended Security Best Practices**

- Use strong, unique credentials for --rc-user / --rc-pass  
- Restrict access via:
    - Narrow IP whitelist in AWS Security Group, or   
    - Bind to specific IP: `--rc-addr=<your_ip>:5572`  
- To secure traffic, consider adding HTTPS via a reverse proxy (e.g., Nginx + TLS) or services like Cloudflare Tunnel    

---
### Run Rclone rcd as a systemd Service

To keep the Rclone daemon (`rcd`) running in the background even after reboots, you can register it as a systemd service on your Linux system (such as Ubuntu EC2 instance).
- It will start automatically on system boot.
- It runs reliably in the background with automatic restarts on failure.

---

#### 1. Create a systemd Service File

Create the following file:

````

```bash
sudo nano /etc/systemd/system/rclone-rcd.service
````

Paste the following content (adjust your rc-user, rc-pass, and any flags as needed):

```
[Unit]
Description=Rclone Remote Control Daemon
After=network-online.target

[Service]
User=ubuntu
ExecStart=/usr/bin/rclone rcd \
  --rc-user=admin \
  --rc-pass=admin \
  --rc-addr=0.0.0.0:5572 \
  --rc-web-gui \
  --log-file=/var/log/rclone.log \
  --log-level=INFO
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

> 🔒 **Security Note**: Change the admin credentials to something secure in production environments.

---

#### 2. Reload systemd and Enable the Service

```
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable rclone-rcd
sudo systemctl start rclone-rcd
```

---

#### 3. Verify Status

To confirm that the daemon is running:

```
sudo systemctl status rclone-rcd
```

You should see active (running) in green.

---


With these steps, your Rclone daemon runs in the cloud, fully accessible via RcloneView or other clients—ready to efficiently manage your remote storage from anywhere.