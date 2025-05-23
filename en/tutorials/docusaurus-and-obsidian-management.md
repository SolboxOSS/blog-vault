---
sidebar_position: 1
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

목차 및 개요

- 개요: 
	- docusaurus의 용도 및 SSG 로서의 명성 간략히 1~2줄 요약
	- Obsidian의 용도 및 명성 간략히 1~2줄 요약
	- 기술블로그 사이트를  제작하는데 있어서 왜 docusaurus와 Obsidian 조합이 필요한지 간략히 설명
	- RcloneView의 Folder Compare 기능으로 Obsidian과 Docusaurus 간 파일을 관리하고, 동일하게 유지하는 장점을 설명.
- 시스템 구성도
	- Obsidian - RcloneView(Folder Comparison and File 동기화 ) - Docusaurus
- 운영방법
	- Obsidian으로 마크다운 페이지 작성 -> RcloneView로 비주얼하게 Docusaurus 저장소 내용과 비교 -> 업데이트 혹은 새로 작성된 페이지만 복사 -> Docusaurus로 build 및 페이지 게시.
	- Obsidian 과 Docusaurus의 각 저장소의 폴더구조와 폴더명을 다르게 운영하면서, 서로 다른 이름의 폴더의 내용은 동일하게 유지해야할 필요가 있음.
	- 예, Static image의 경우 Docusaurus에서 최종 SSG 로 만든 이미지는 baseURL로  바뀌며, 이를 위해 Obsidian에서는 최종 baseURL 기반으로 폴더를 관리해야함. 그러나 Docusaurus 소스폴더는 /Static/ 아래에 이미지를 저장하므로, Docusaurus와 obsidian의 Static Image 폴더명은 다르게 유지관리해야 함.
- RcloneView를 이용한 Obsidian 저장소와 Docusaurus 저장소 비교 방법
	- 1. Combine 리모트 생성
	  - 각 저장소에서 서로 다른 위치와 이름의 폴더들을 동일한 내용으로 유지하기 위해,각 저장소의 동기화 매칭해야할 폴더를 Rclone Combine을 이용해 각 폴더를 동일한 이름으로 변경하여 리모트를 생성. 
	  예) 아래와 같이 

| Obsidian 폴더     | Obsidian Combined 폴더 | Docusaurus Combined 폴더 | Docusaurus 폴더   |
| --------------- | -------------------- | ---------------------- | --------------- |
| /support/images | /images              | /images                | /static/images  |
| /en/howto       | /howto               | /howto                 | /doc/howto      |
| /en/tutorials   | /tutorials           | /tutorials             | /blog/tutorials |
	- 최종적으로 Obsidian의 Combine remote와 Docusaurus의 Combine remote 내의 폴더명으로 동일하게 하여 두 저장소를 동기화하는 방식으로 만듬.
	  (그러나, 각 저장소의 실제는 다른 폴더가 동일한 파일 내용으로 동기화 관리되는 것임.)
	- 
