## **🧩 Title**

  

Batch Job Processing – Chain Multiple Jobs into One Flow

---

## **📄 Description**

  

Introduce a **Batch Job feature** that allows users to group and execute multiple RcloneView jobs — **sequentially or in parallel** — as part of a single operation.

  

This enables **automated workflows** like:

- Copy → Sync → Purge
    
- Move to Cloud A → Backup to Cloud B
    
- Delete temp → Copy fresh content → Notify on Slack
    

  

A Batch Job acts like a **“playlist” of jobs**, preserving their order and type, with unified status tracking and error handling.

---

## **🛠️ Usage Scenarios**

1. **Daily Production Archive**
    
    - Copy from local drive → primary cloud (Dropbox)
        
    - Move processed files to cold storage (Backblaze B2)
        
    - Purge temp folder after success
        
    
2. **Multi-cloud Sync with Cleanup**
    
    - Sync main documents folder to OneDrive
        
    - Delete legacy files from Google Drive
        
    - Copy same data to a USB path as local backup
        
    
3. **Safe Transfer with Final Cleanup**
    
    - Copy → Verify (planned) → Purge source
        
    

  

Each step would execute in order and report its result individually, with the entire batch treated as a single unit.

---

## **🧪 Reference UI**


---

## **⚠️ Limitations to Overcome**

| **Current Limitation**                    | **Clarification**                                          |
| ----------------------------------------- | ---------------------------------------------------------- |
| RcloneView runs single jobs independently | No native support for sequential/conditional job execution |
| No “Job dependency” logic yet             | Requires UI and backend to manage job groups and order     |
| Error handling between jobs unclear       | Need toggle: continue on error vs. stop on failure         |

---

## **📅 Roadmap (Vision)**

- ✅ Design Batch Job structure (with name, description, job list, run mode)
    
- 🧩 Support **manual run + per-job status tracking**
    
- 🔁 Add **“Run jobs sequentially”** vs. **“Run in parallel”** toggle
    
- 🛑 Option: Stop batch on first failure or continue regardless
    
- 📆 (Future) Schedule Batch Jobs just like normal jobs
    
- 📤 (Future) Export/Import batch templates (.json)
    

---

## **🙋‍♀️ Want this feature?**

  

Upvote this post if you want to create **powerful, multi-step workflows** inside RcloneView using Batch Jobs!

  

Which combinations of jobs would you automate? Share your ideas below 👇