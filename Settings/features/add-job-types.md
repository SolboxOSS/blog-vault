## **🧩 Title**

  

Support More Job Types: Copy, Move, Delete, Purge (Beyond Sync)

---

## **📄 Description**

  

RcloneView currently supports **Sync** and **Bi-Directional Sync** operations.

We’re now planning to expand to a wider range of **Job Types**, including:

- 📄 **Copy** – One-way file duplication without deletion (coming next sprint)
    
- 🚚 **Move** – Copy then delete source (useful for organizing cloud storage)
    
- ❌ **Delete** – Remove files from a specific path or remote
    
- 🧹 **Purge** – Hard-delete entire folders (no trash, no versioning)
    

  

Each operation serves a **distinct use-case** and allows users more control over their file management strategy.

---

## **🛠️ Usage Scenarios**

- ✅ **Copy**
    
    A user wants to back up local files to both Dropbox and Google Drive — without affecting the source files.
    
    → Copy ensures one-way backup with zero risk of source loss.
    
- ✅ **Move**
    
    A user wants to transfer processed files to cold storage (e.g., from NAS to B2).
    
    → Move clears up local space after cloud transfer.
    
- ✅ **Delete**
    
    A user cleans up temporary logs or cache directories in a scheduled job.
    
    → Delete removes specific file types from a cloud path.
    
- ✅ **Purge**
    
    A user wants to remove an entire backup folder from a cloud remote after archiving.
    
    → Purge removes all files instantly, including any leftover metadata or empty dirs.
    

---

## **🧪 Reference Behavior**

- rclone copy – preserves source, overwrites target if changed
    
- rclone move – equivalent to copy + delete
    
- rclone delete – deletes file(s) at target path only
    
- rclone purge – aggressively deletes folder + all contents
    

  

These are standard Rclone commands, but not yet exposed in RcloneView via UI workflows.

---

## **⚠️ Limitations to Note**

| **Current Limitation**                                    | **Clarification**                                            |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| **Copy** is coming in the next sprint                     | UI and logging logic being finalized                         |
| **Move/Delete/Purge** may require confirmation safeguards | Extra UX validation is needed to prevent accidental deletion |
| Not all remotes support purge                             | Rclone will fallback to recursive delete if unsupported      |

---

## **📅 Roadmap (Vision)**

- ✅ Add Copy as a selectable Job Type (next sprint)
    
- 🔜 Add Move with visual confirmation of delete-on-source
    
- 🗑 Introduce Delete and Purge with “Dry Run” preview mode
    
- 🔐 Add **safety toggles** (e.g., “require confirmation for destructive jobs”)
    
- 🔁 Allow batch job templates with mixed job types
    

---

## **🙋‍♂️ Want this feature?**

  

Upvote this post if you want **more flexible job types** beyond Sync — like Copy, Move, or Purge — directly in RcloneView!

Have a specific use-case for these operations? Let us know below 👇