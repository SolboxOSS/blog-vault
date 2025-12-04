---
title: "A Surprisingly Great Tool for Multi‑Cloud Storage – RcloneView Review"
tags: [rclone, cloud-storage, nas, devtool, review]
---

I’ve been using a **Synology NAS** at home for quite a while.  
It’s connected over SMB, and I’ve never really had issues with it.  
Even when I’m outside, I can easily browse my photos and videos using Synology’s mobile apps.

But recently my work started involving multiple cloud platforms like **Google Drive, AWS S3, and Cloudflare R2**.  
Suddenly I needed a single place to manage them all — and sometimes even back up data to my Synology NAS.

That’s when I discovered **Rclone**.  
It’s powerful, but since it’s a **CLI‑based tool**, it wasn’t very friendly for someone like me.  
So I started looking for a GUI frontend and found **RcloneView** — and wow, this tool really made my life easier.

It’s still a relatively new app, so the UX and feature set are evolving.  
But if you want to manage **multiple clouds and NAS in one place**, it’s already incredibly useful.

---

## Installation and First Impressions

I downloaded it from [rcloneview.com/download](https://rcloneview.com/src/download).
I’m using the **Windows version**.

After installation I launched it — and boom.
RcloneView immediately detected my **Synology NAS** on the local network and asked if I wanted to connect.
That was a really nice first impression.

![Synology NAS auto-detected and WebDAV connection option](attachments/Pasted%20image%2020251117224304.png)

**WebDAV setup**  
Since I also need to access my NAS from outside my home, I chose a **WebDAV** connection — easy and stable.
In the WebDAV setup dialog, I simply gave the remote a name, entered the NAS WebDAV URL, and filled in my username and password — that was enough to connect from anywhere.

If you want a more detailed walkthrough (including all the optional fields),
see: [WebDAV](https://rcloneview.com/support/howto/remote-storage-connection-settings/webdav).

![Adding a WebDAV remote in RcloneView](attachments/Pasted%20image%2020251117224422.png)

Then I connected my **Google Drive**, **AWS S3**, and **Cloudflare R2** one by one.
The setup for each provider was smooth, with a clear step‑by‑step wizard.

**Google Drive setup**

In RcloneView you just pick **Google Drive** from the provider list, give the remote a name, and follow the browser login flow.

![Adding Google Drive remote in RcloneView](attachments/Pasted%20image%2020251107235650.png)

**Amazon S3 setup**

For **AWS S3**, select the S3 provider, paste your Access Key / Secret Key, choose the region, and you’re good to go.
More detailed S3 configuration (including S3‑compatible providers) is covered here:
[AWS S3 and S3‑Compatible](https://rcloneview.com/support/howto/remote-storage-connection-settings/s3).
If you’re not sure how to get your keys and region, see:
[How to Get Your AWS Access Key and Region for Rclone](https://rcloneview.com/support/howto/cloud-storage-setting/aws-account-info).

![Adding Amazon S3 remote in RcloneView](attachments/Pasted%20image%2020251114160809.png)

**Cloudflare R2 setup**

For **Cloudflare R2**, RcloneView treats it as an S3‑compatible storage: you enter the access key, secret key, and R2 endpoint.
There’s a separate how‑to that walks through getting those values from the Cloudflare dashboard:
[How to Obtain Cloudflare R2 Credentials and Endpoint](https://rcloneview.com/support/howto/cloud-storage-setting/cloudflare-r2-credential).

![Adding Cloudflare R2 remote in RcloneView](attachments/Pasted%20image%2020251114160846.png)


## Managing Multiple Clouds in One View

Once all the connections were ready, I could see everything side‑by‑side.
RcloneView pins the **Local Disk** on the left panel (you can’t move that),
but you can rearrange your cloud tabs however you like. Nice touch.

![Local, NAS, and clouds shown side‑by‑side](attachments/Pasted%20image%2020251113170651.png)

Now I can browse **Google Drive, Synology NAS, Cloudflare R2, AWS S3, and my local folders** in a single app.
This alone already saves me a lot of time.

File operations are just drag & drop — very similar to Windows Explorer.
Copying between different clouds feels completely natural.  


## Handy Tricks: Alias & Quick Access

For folders I use often, I click the **Alias (Star)** icon (like a bookmark).
This creates a shortcut to that specific folder,
so I don’t have to dig deep through the directory tree every time.

Rclone calls these “Alias remotes,”
but you can just think of them as **Favorites** or **Quick Access** folders.  

![Creating an alias (favorite) for a frequently used folder](attachments/Pasted%20image%2020251113170240.png)

---

## My Real Use Case: How RcloneView Fits Around My Static Site

This diagram is basically my daily workflow in one picture.
RcloneView on my laptop sits in the middle and connects my **local repository (disk)** with  
**AWS S3**, **Synology NAS**, **Google Drive**, and **Cloudflare R2**.  

![](attachments/Pasted%20image%2020251117234633.png)

- I develop the site in a **local Git repository** on disk.
- RcloneView syncs that local build to **AWS S3** for **web preview**.
- At the same time, it keeps instant backups on **Synology NAS** and **Google Drive** using a **1:2 Sync** job.
- Separately, a **scheduled Sync job** pushes the same local repository to **Cloudflare R2** as an off‑site backup.  

RcloneView itself never publishes the website; it focuses on preview and storage.  

### 1. Previewing the Site on AWS S3

When I want to preview changes, I open the local repository on the left and the S3 bucket on the right,
then use either **Compare + Copy** or **Sync**.  

For small edits, **Compare** shows exactly which files are new or modified.
I select just those items and click **Copy** — this updates my **S3 preview site** without touching everything else.  

This saves a ton of time because it doesn’t re‑upload unchanged files.
If there are *thousands of files*, the comparison itself can still take a while, but it’s usually worth it.  

![Comparing folders before copying only changed files](attachments/Pasted%20image%2020251114162605.png)

If you want a step‑by‑step walkthrough of the Compare feature,
see: [Compare folder contents](https://rcloneview.com/support/howto/rcloneview-basic/compare-folder-contents).  

When there are a lot of changes, I simply create an **instant Sync job** like the one below  
and let RcloneView update the S3 bucket in one shot.  

![Sync job configuration in RcloneView](attachments/Pasted%20image%2020251114164156.png)

### 2. Instant 1:2 Backup to Synology NAS and Google Drive

I don’t want my local repository to be a single point of failure.
So I created a **1:2 Sync** job in RcloneView with:  

- **Source**: local repository on disk
- **Destination 1**: **Synology NAS**
- **Destination 2**: **Google Drive**   

With one click, the same folder is synced to both destinations.
This gives me a fast local backup (NAS) and a cloud backup (Google Drive) at the same time.  

![Configuring sync from local homepage to multiple destinations](attachments/Pasted%20image%2020251114165630.png)

For more details on how instant sync between multiple remotes works,
check: [Synchronize Remote Storages Instantly](https://rcloneview.com/support/howto/rcloneview-basic/synchronize-remote-storages).

While a sync is running, the **Transfer** panel at the bottom shows live progress —  
file counts, speed, and estimated time. It’s surprisingly satisfying to watch. 😎

![Transfer panel showing live sync progress](attachments/Pasted%20image%2020251114164249.png)

When I’m happy with an instant sync setup like this, I click **Save to Jobs**.
The job is stored in the **Job Manager**, so I can re‑run or tweak it anytime without re‑configuring everything.  

![Saved sync jobs listed in Job Manager](attachments/Pasted%20image%2020251117181845.png)

If you’re curious about creating and managing jobs,
there’s a dedicated guide: [Create Sync jobs](https://rcloneview.com/support/howto/rcloneview-basic/create-sync-jobs).  

### 3. Scheduled Off‑Site Backup to Cloudflare R2

For disaster‑recovery style backups, I use **Cloudflare R2**.
Here again the **source** is the local repository on disk, but this time I create a dedicated job:  

- **Source**: local repository
- **Destination**: Cloudflare R2 bucket (backup only)  

Then I enable a **schedule** so this job runs automatically — e.g. once a day.  

In the screenshot below, I’m scheduling a backup to run at **00:10** every **Monday, Wednesday, and Friday**.
RcloneView uses a **crontab‑style syntax**, so you can describe very precise schedules.
At first that syntax looks a bit intimidating, but there’s a built‑in **Simulator**  that shows the next run times, so it’s easy to verify that you got it right.  

![Setting up a scheduled backup job with crontab-style syntax and simulator](attachments/Pasted%20image%2020251117181605.png)

The execution history for each scheduled job is also available from the Job Manager.
Click the **History** icon to see when the job ran, how long it took, how many files were transferred, and whether it completed successfully.  

![Viewing execution history for a scheduled Cloudflare R2 backup job](attachments/Pasted%20image%2020251117181501.png)

If you want to go deeper into automated scheduling,
the advanced docs cover it in detail:
[Job scheduling and Automated Execution](https://rcloneview.com/support/howto/rcloneview-advanced/job-scheduling-and-execution).

It’s a bit disappointing that this scheduling feature is only available on the paid tier,
but even with the free plan you can still run manual backups easily using **Sync**.  


---

## Pros, Cons, and Who It’s For

**What I like**

- Clean, visual interface for Rclone’s powerful features
- Easy setup for multiple providers (Google Drive, S3, R2, NAS, etc.)
- Drag‑and‑drop transfers between any two remotes
- Helpful tools like **Compare**, **Sync**, and **Alias** favorites
- Transfer panel with clear progress and speed information  

**Things that could be better**

- Folder comparison can be slow on very large directories
- Some advanced options still feel a bit technical if you’re not familiar with Rclone
- Scheduling is locked behind a paid plan (though understandable)  

---

## Final Thoughts

If you manage multiple clouds or NAS systems, **RcloneView** is absolutely worth checking out.  

RcloneView makes multi‑cloud storage management feel almost effortless.
It bridges the gap between power users who know the Rclone CLI  and everyday users who just want a reliable, visual interface.  

Sure, there’s room for improvement —  
faster folder comparison, more polished UI, maybe richer scheduling options.
But even now, it’s already one of the most **practical hybrid‑cloud managers** I’ve tried.  

Try it yourself at 👉 [https://rcloneview.com](https://rcloneview.com)
