## **🧩 Title**

  

**Instagram Photo Archiving to Remote storage**

---

## **📄 Description**

  

Many users, creators, and archivists want to **preserve Instagram content**—their own uploads, brand media, or curated inspirations—into personal cloud storage.

  

We’re exploring a new feature to allow RcloneView to:

- 📥 **Crawl Instagram photos** from public or authenticated profiles
    
- 🗂️ Organize them by date or post ID
    
- ☁️ Download them to any remotes (Local disk, Dropbox, Google Drive, etc.)
    
   
---

## **⚠️ Important Limitations (Please Read)**

| **❗ Constraint**                                            | **⚙️ Notes**                                                               |
| ----------------------------------------------------------- | -------------------------------------------------------------------------- |
| Rclone does **not** support Instagram                       | This is **not part of official Rclone remotes**                            |
| Instagram API is **limited** and requires login/auth scopes | We may need to use **3rd-party scraping libraries** or reverse engineering |
| Terms of Service may limit automated scraping               | **We will NOT enable public scraping without user consent or compliance**  |

📌 For these reasons, this feature would require a **RcloneView-native implementation**, and likely involve:

- ⏳ Extensive technical research
    
- 🔐 OAuth integration or browser session-based crawling
    
- 🧠 Media parsing & metadata extraction
    
- 🚧 Continuous maintenance due to API/website changes
    

**This would be a long-term R&D project.**

---

## **🛠️ Potential UX Scenario**

1. User enters their Instagram account or target public profile
    
2. RcloneView shows available media items (thumbnails, captions, dates)
    
3. User selects items to download
    
4. RcloneView downloads media and saves to the configured cloud destination

---

## **📅 Roadmap**

- 🔬 Phase 0: Technical feasibility research (instaloader, puppeteer, Graph API)
    
- ⚖️ Phase 1: Legal review & user-consent policy
    
- 🧪 Phase 2: MVP prototype with manual download and sync
    
- ⏳ Phase 3+: UI integration, scheduling, tagging
    

---

## **🙋‍♀️ Is This Useful to You?**

  

If you’d like to see **Instagram-to-Remote storage archiving** in RcloneView, please **upvote this feature**.

  

We’ll use your interest to decide whether to **invest R&D time** in this long-term project.

  

Also, share below:

- What kinds of Instagram content would you archive?
    
- Do you already use 3rd-party tools? Which ones work best for you?
    

  

👇 Let’s build the future of cloud media archiving together.