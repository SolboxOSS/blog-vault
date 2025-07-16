---
sidebar_position: 9
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
date: 2025-07-15
author: Jay
---

External Rclone을 이용시 현재 PC의 로컬 폴더를 External Rclone으로 Upload하는 오류를 방지하기 위한 루틴을 설명한다. 

예) PC 로컬 폴더 -> External Rclone -> AWS S3 업로드  (실패) 왜냐하면 External Rclone의 입장에선 로컬이 PC 로컬 폴더가 아니라 External Rclone이 동작하는 서버의 로컬디스크 이므로 

PC로컬 폴더 -> Embedded Rclone -> AWS S3 업로드 (성공)
즉, Embedded Rclone 이용 



따라서, Extrernal Rclone 을 이용하면서 PC 로컬폴더 -> Cloud Remote 1 -> Cloud Remote2 의 과정을 오류 없이 수행하려면,

PC 로컬폴더 -> Embedded Rclone -> Cloud Remote1  업로드 완료 후

Cloud Remote1 -> External Rclone -> Cloud Remote2 로 이동.

하는 3-way 방식을 사용해야 함을 설명한다.