---
sidebar_position: 2
description: This is sample Post for writer
keywords:
  - rcloneview
  - howto
  - cloud
  - sync
  - rclone
tags:
  - RcloneView
  - howto
  - Cloud
  - Sync
date: 2025-05-23
author: Jay
---
# Managing Files Between Obsidian Markdown tool and Docusaurus SSG(Static Site Generator)

# Overview

**Docusaurus** is a widely adopted static site generator (SSG) known for its simple setup and powerful documentation features, making it ideal for building technical blogs and developer portals.
  
**Obsidian** is a popular markdown-based knowledge management and writing tool favored by developers, researchers, and writers for its extensibility and intuitive local editing capabilities.

When building a high-quality technical blog site, combining Obsidian for writing and Docusaurus for publishing provides an ideal workflow. Obsidian ensures smooth offline content creation, while Docusaurus allows for structured, SEO-optimized web publishing.

**RcloneView**, a GUI client for Rclone, offers an intuitive folder comparison and sync feature. It makes it easy to visually manage and synchronize the folder structures between your Obsidian workspace(vault) and Docusaurus source directory—ensuring consistency without overwriting important structure differences.

Here is the first draft of your technical documentation in English based on the planning structure you provided. I’ve also included improvement suggestions at the end.

## System Architecture

```
Obsidian Vault
    ↓
(RcloneView Folder Comparison & Sync)
    ↓
Docusaurus Project Folder
```

Obsidian and Docusaurus are treated as separate repositories with independent folder names and structures. RcloneView bridges the gap by mapping and synchronizing matched folders between them using visual comparison and synchronization.

## **Operation Workflow**

1. **Write Markdown content in Obsidian**.
2. **Use RcloneView to compare** the Obsidian vault folders and the Docusaurus content folders visually.
3. **Synchronize only newly added or updated files** from Obsidian to the Docusaurus directory using selective sync.
4. **Build and deploy the site** using Docusaurus build and publish commands.

### **Folder Structure Differences and Mapping**

  Because Docusaurus and Obsidian often have different organizational needs, it is essential to maintain different folder names but ensure synchronized content. For example:

- Obsidian may manage image folders using a base URL-style structure.
- Docusaurus requires static images to be stored under /static/.  

Thus, the folders must be logically mapped but physically distinct.

## Synchronizing Obsidian and Docusaurus Repositories with RcloneView

### 1. Creating a Combine Remote
  
To maintain identical folder structures despite different source paths, you can use **Rclone Combine remotes**. This allows you to unify and present differently-named source folders under a common virtual structure.

Below is an example of a Combine remote setup:

| **Obsidian Folder** | **Obsidian Combined Folder** | **Docusaurus Combined Folder** | **Docusaurus Folder** |
| ------------------- | ---------------------------- | ------------------------------ | --------------------- |
| /support/images     | /images                      | /images                        | /static/images        |
| /en/howto           | /howto                       | /howto                         | /docs/howto           |
| /en/tutorials       | /tutorials                   | /tutorials                     | /blog/tutorials       |

With this configuration:

- Obsidian’s /support/images is shown as /images via Combine remote.
- Docusaurus’s /static/images is also mapped to /images.
- You can now compare /images in both remotes using RcloneView and sync them accordingly.

## **Improvement Suggestions**

1. **Illustrate the Architecture**: Add a visual diagram (e.g., in SVG or PNG format) showing the data flow between Obsidian → RcloneView → Docusaurus.
2. **CLI Alternative**: For advanced users, briefly describe how to use rclone sync or rclone bisync for the same task.
3. **File Type Filtering**: Mention how RcloneView can exclude unnecessary files (e.g., .DS_Store, .obsidian/, or .git/) using filters or .rcloneignore.
4. **Markdown Compatibility Tips**:
    - Ensure Obsidian markdown syntax is compatible with Docusaurus Markdown rendering (especially for images and frontmatter).
    - Add a table mapping supported syntax and limitations.
5. **Automation Tip**: Suggest how to script the folder sync process using RcloneView’s CLI if batch updates are frequent.  

Would you like me to help create the folder mapping config for Combine remotes in rclone.conf format or add screenshot mockups?

- 시스템 구성도
	- Obsidian - RcloneView(Folder Comparison and File 동기화 ) - Docusaurus
- 운영방법
	- Obsidian으로 마크다운 페이지 작성 -> RcloneView로 비주얼하게 Docusaurus 저장소 내용과 비교 -> 업데이트 혹은 새로 작성된 페이지만 복사 -> Docusaurus로 build 및 페이지 게시.
	- Obsidian 과 Docusaurus의 각 저장소의 폴더구조와 폴더명을 다르게 운영하면서, 서로 다른 이름의 폴더의 내용은 동일하게 유지해야할 필요가 있음.
	- 예, Static image의 경우 Docusaurus에서 최종 SSG 로 만든 이미지는 baseURL로  바뀌며, 이를 위해 Obsidian에서는 최종 baseURL 기반으로 폴더를 관리해야함. 그러나 Docusaurus 소스폴더는 /Static/ 아래에 이미지를 저장하므로, Docusaurus와 obsidian의 Static Image 폴더명은 다르게 유지관리해야 함.
- RcloneView를 이용한 Obsidian 저장소와 Docusaurus 저장소 비교 방법
	- 1. Combine 리모트 생성
	  - 각 저장소에서 서로 다른 위치와 이름의 폴더들을 동일한 내용으로 유지하기 위해,각 저장소의 동기화 매칭해야할 폴더를 Rclone Combine을 이용해 각 폴더를 동일한 이름으로 변경하여 리모트를 생성. 
	  예) 아래와 같이  최종적으로 Obsidian의 Combine remote와 Docusaurus의 Combine remote 내의 폴더명으로 동일하게 하여 두 저장소를 동기화하는 방식으로 만듬.
	  (그러나, 각 저장소의 실제는 다른 폴더가 동일한 파일 내용으로 동기화 관리되는 것임.)
	- 

| Obsidian 폴더     | Obsidian Combined 폴더 | Docusaurus Combined 폴더 | Docusaurus 폴더   |
| --------------- | -------------------- | ---------------------- | --------------- |
| /support/images | /images              | /images                | /static/images  |
| /en/howto       | /howto               | /howto                 | /doc/howto      |
| /en/tutorials   | /tutorials           | /tutorials             | /blog/tutorials |
	-
