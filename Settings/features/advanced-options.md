## **🧩 Title**

  

Advanced Rclone Settings for Power Users – Performance & Limitation Control

---

## **📄 Description**

  

Introduce a **dedicated Advanced Options panel** in RcloneView that allows users to configure commonly used **performance tuning** and **cloud-specific limitation** flags when running Sync or Copy(upcoming) jobs.

  

This empowers more experienced users to fine-tune RcloneView without needing to drop down to the command line.

---

### **🔧 Examples of Supported Options**

  
#### **🚀 Performance Tuning**

- --tpslimit – Limit transactions per second (important for API rate limits)
    
- --buffer-size – Per-transfer buffer size (e.g., 16M)
    
- --drive-chunk-size – Chunk size for Google Drive uploads
    

  
#### **🌩️ Cloud-Specific Controls**

- --s3-upload-concurrency
    
- --b2-chunk-size
    
- --dropbox-batch-mode
    
- --onedrive-chunk-size
    
- --max-transfer – Stop transfers when total reaches a specified size
    

  
These options can significantly improve stability and performance when transferring large datasets or syncing across providers with rate limits.

---

## **🛠️ Usage Scenarios**

- A user syncing from **Google Drive → Dropbox** encounters frequent throttling.
    
    → They adjust --tpslimit to avoid 429 errors.
    
- Another user backing up to **Backblaze B2** wants faster uploads.
    
    → They increase --b2-chunk-size and --transfers for better throughput.
    
- A team sharing a remote workspace wants to limit **daily bandwidth**.
    
    → They enable --max-transfer to stop jobs after hitting 100GB.
    

---

## **⚠️ Limitations to Overcome**

| **Issue**                                                  | **Clarification**                                                             |
| ---------------------------------------------------------- | ----------------------------------------------------------------------------- |
| 🛠️ Not all CLI options are supported in API of RcloneView | RcloneView uses **Rclone API**, not raw CLI execution                         |
| ⚠️ Settings apply globally                                 | Advanced options are **applied to remotes**, not individual jobs              |
| 🔄 Dynamic job-level tuning is not available yet           | Per-job overrides will require deeper integration or wrappers                 |
| 📉 Some options may be silently ignored                    | Unsupported flags will be skipped without CLI validation unless handled in UI |

---

## **📅 Roadmap (Vision)**

- ✅ Add Advanced Options config per remote (via Rclone API options.set)
    
- 🧠 Auto-suggest options based on selected cloud provider (e.g., show --drive-chunk-size only for Google Drive)
    
- 🧪 Validate user input for numerical/size formats
    
- ⛓ Future: Allow **job-level overrides** via embedded wrapper logic
    

---

## **🙋‍♀️ Want this feature?**

  

Upvote this post if you’d like to have **fine-grained control over Rclone’s engine** right inside RcloneView — no terminal required!

Have favorite Rclone options you want to see? Share your must-have flags in the comments 👇
