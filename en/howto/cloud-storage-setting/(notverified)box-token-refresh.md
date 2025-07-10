---
sidebar_position: 4
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
date: 2025-06-10
author: Jay
---
# Box Token Referesh

Rclone 은 Box의 경우 Token의 유효기간이 60일이어서 Referesh를 해주어야 합니다. 
60일 이상 사용 시 기간이 지나면 RcloneView에서 파일은 보이나 지우기 등의 작업에서 오류가 발생할 수 있습니다.

오류가 발생 시 아래의 방법으로 Token Refresh를 수행하시길 바랍니다. 

Referesh 하는 방법은 다음과 같습니다.

step1. Box 리모트 편집을 수행합니다. 

Refersh 전 Token



