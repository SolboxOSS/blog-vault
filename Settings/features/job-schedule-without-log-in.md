## **🧩 Title**

  

**Run Scheduled Jobs Without User Login – Background Mode**

---

## **📄 Description**

  

Many users want their scheduled jobs (e.g., backup or sync tasks) to run **even when they’re not logged into the OS**, especially for server-style setups or unattended environments.

  

This feature would allow RcloneView’s **Job Scheduler** to execute tasks:

- ✅ On boot, **before login**
    
- ✅ In full background, **without opening the GUI**
    
- ✅ With minimal system overhead
    

  

This could help scenarios like:

- 🖥️ Personal PC auto-backups overnight
    
- 📦 Headless servers performing sync jobs
    
- 🏢 Office computers maintaining scheduled jobs without user sessions
    

---

## **⚠️ Important Technical Notes**

  

> This feature is **under investigation** and may not be technically feasible in all environments. We want to be transparent about the **limitations**.

|**Environment**|**Limitation**|
|---|---|
|🪟 Windows|Running background services **without login** often requires [service manager](https://nssm.cc/) support or task scheduler + system permissions. GUI apps like RcloneView may not load fully in background mode.|
|🐧 Linux/macOS|More flexible with systemd, launchd, or cron, but still **requires CLI-based execution**, not full GUI mode.|

We may explore **delegating scheduled jobs to an embedded service agent**, but this introduces **security**, **permission**, and **architecture** challenges.

---

## **🛠️ Usage Scenarios**

1. You schedule a daily sync between your NAS and Dropbox at 3am.
    
2. Even if no user is logged in, the job still runs as expected.
    
3. Logs are available later when the user opens RcloneView.
    

---

## **🧪 Reference GUI**


---

## **📅 Roadmap**

- 🔬 Investigate Windows service compatibility (e.g., via NSSM or Task Scheduler)
    
- 📦 (Optional) Create a **headless RcloneView Agent** for background scheduling
    
- 🔐 Define permission model and system-level logging strategy
    
- ❌ If infeasible, provide CLI-based guidance instead (e.g., .bat/.sh for Rclone)
    

---

## **🙋‍♂️ Want this feature?**

  

This is a technically challenging request, but if **headless job execution** is something you need, please **upvote** this post!

  

Have experience running background jobs with Rclone or other tools?

👉 Share your setup in the comments to help shape this feature!
