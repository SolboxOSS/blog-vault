## **🧩 Title**

  

**Preview PDF, Image, and Document Files in RcloneView**

---

## **📄 Description**

  

Currently, RcloneView focuses on file transfer, sync, and cloud management. However, many users managing **cloud content** want to **quickly preview files** before downloading or processing them.

  

This feature would add built-in support for **file previewing**, including:

- 🖼️ **Images** (e.g., JPG, PNG, GIF, etc.)
    
- 📄 **PDF documents** (e.g., manuals, reports)
    
- 📝 **Text files** (e.g., .txt, .md, .log)
    
- (Optional) **Office docs** like .docx, .xlsx, .pptx via cloud-based renderers
    

  

This would help users:

- ✅ Confirm file contents before running a sync or delete job
    
- ✅ Quickly browse remote folders (especially image/PDF heavy folders)
    
- ✅ Reduce unnecessary downloads
    

---

## **🛠️ Usage Scenarios**

1. User browses a Dropbox or Google Drive folder in RcloneView.
    
2. They hover over or click a .pdf or .jpg file.
    
3. A preview pane (or popup modal) shows the file contents, rendered directly.
    
4. The user can decide whether to download, sync, or ignore the file.
    

---

## **🧪 Reference UI **

---

## **⚠️ Limitations to Consider**

| **Limitation**                           | **Proposed Approach**                                                     |
| ---------------------------------------- | ------------------------------------------------------------------------- |
| Rclone CLI doesn’t support previewing    | Use RcloneView’s GUI to fetch and render files using temp download buffer |
| Previewing large files is slow           | Add size limit (e.g., only < 10MB files)                                  |
| Proprietary formats (e.g., .docx, .xls)  | Use optional 3rd-party viewer integrations                                |
| Security concern for previewing binaries | Restrict preview to file types: PDF, TXT, JPG, PNG                        |

---

## **📅 Roadmap (Proposal)**

- ✅ PDF & Image preview using in-app rendering
    
- ⏳ Text preview with syntax highlighting
    
- 🧪 Evaluate docx/xlsx preview via Google Docs Viewer or LibreOffice integration
    
- 📦 Add “Preview” toggle option in file browser UI
    

---

## **🙋‍♀️ Want this feature?**

  

If **previewing files directly in RcloneView** would improve your workflow, please **upvote this feature**!

  

Got preferred file types or viewer libraries to recommend?

Drop your ideas in the comments 👇
