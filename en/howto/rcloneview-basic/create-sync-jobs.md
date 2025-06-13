---
sidebar_position: 5
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
date: 2025-06-04
author: Jay
---
# Create Sync jobs

자주 사용하는 Sync 타스크를 Job으로 생성하고, 반복되는 Job을 한번의 클릭으로 수행할 수 있다. 또한, 일정시간에 자동으로 실행할 수 있도록 스케줄링할 수 있도록 하는 편의성을 제공합니다. 


:::info You need PLUS license to schedule jobs
Job 스케쥴링 기능 사용을 위해서는 PLUS 라이선스가 필요합니다. 
:::

Job을 생성하는 방법은 두가지가 있습니다. Instant Sync 타스크로 부터 Job을 생성하는 방법과 Job Manager를 이용하여 Job을 생성하는 방법이 있습니다.

## Sync로 부터 Job 생성하기

Home menu의 Sync 툴바를 이용해 Sync 타스크를 설정 후 Save to Jobs를 이용해 Job을 생성할 수 있습니다. {{링크 달기}}

You can view and run saved jobs by clicking the **`Job Manager`** toolbar in the Home menu.

## Job Manager를 이용하여 Job 생성하기


### Sync 대상 Remote의 폴더를 지정하기 (Optional Operation)




### Job Manager로 Job 생성하기




## Job 수행 하기

### Job 수행하기


### dry-run으로 시뮬레이션 하기 (Optional Operation)





## Job 히스토리 보기





## Job 관리하기

RcloneView - advanced



## Sync 대상 리모트 및 폴더 선택 하기.

- Remote Explorer 창의 폴더 트리뷰에서 싱크 대상 폴더를 선택한다. 혹은 Explorer 패널의 Path Bar에 직접 대상 폴더를 입력해도 된다.
	- 왼쪽 Explore 패널의 리모트는 Source가 되고, 오른쪽 Explorer 패널의 리모트는 Destination으로 지정되며, Sync Job 창에서 변경이 가능하다.
- 홈메뉴의 Sync 툴바를 클릭하여 Sync 설정을 진행한다. 
<img src="/support/images/en/howto/rcloneview-basic/sync-remote-folder-select.png" alt="sync remote folder select" class="img-medium img-center" />
## Sync 수행하기

- Configure Storages 메뉴에서 소스 리모트 폴더와 목적지 리모트 폴더를 확인/변경 한다.
	- Source와 Destination 설정이 정확한지 확인 후 'Next'를 진행한다.
	- 현재, Sync는 one-direction 싱크를 지원하며, Bidirection은 정식지원이 아닌 beta 버전으로 오류가 많이 발생할 수 있다. 

:::caution How to operate Modifying destination Only
rclone에서지원하는 one-direction sync의 동작은 Source의 내용을 Desination에 완전히 덮어쓰는 미러링 방식의 동기화이다. 따라서, destination에만 존재하는 파일들 삭제되어 지므로 주의해야 한다.
:::

- Advanced Settings 설정은 그대로 두고 다음으로 진행한다.
	- Advanced Setting에서는 리모트간 전송 성능, 무결성 점검 등의 설정을 할 수 있으며, 기본값을 사용하기를 권장하며, 변경을 원할 경우 다음 설명을 참고한다.

- Filtering Settings 설정을 진행한다. 
	- 기존 설정으로 Google Docs, Box Docs등 클라우드기반 파일들은 필터링 하도록 설정되어 있다.
	- 자세한 Filtering Option 설정은 다음 설명을 참고한다.


- Run을 클릭하여 동기화를 수행한다.

<div class="img-grid-3">
<img src="/support/images/en/howto/rcloneview-basic/sync-configure-storage.png" alt="sync configure storage" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-advanced-settings.png" alt="sync advanced settings" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-filtering-settings.png" alt="sync filtering settings" class="img-medium img-center" />
</div>
## 수행결과 확인하기


- 실시간으로 전송중인 파일에 대한 상태 정보를 Transfer 창에서 확인할 수 있다.
	- '+' 버튼을 눌러 전송적인 각 파일별 전송 상태를 모니터링할 수 있다.
<img src="/support/images/en/howto/rcloneview-basic/sync-transfer-window.png" alt="sync transfer window" class="img-medium img-center" />
- 전송이 완료된 각 파일에 대한 전송결과 정보를 Completed 창에서 확인할 수 있다.
	- '+' 버튼을 눌러 전송 완료된 각 파일의 전송결과 정보를 확인할 수 있다.
<img src="/support/images/en/howto/rcloneview-basic/sync-completed-window.png" alt="sync completed window" class="img-medium img-center" />
:::tip Open synchronized remotes by double click on each completed job in Completed window.
Completed 창에서 완료된 Job을 마우스로 더블 클릭하면, explorer 패널에 소스 리모트 폴더와 목적 리모트 폴더를 오픈해서 보여주며, 편리하게 각 동기화 job의 대상 리모트 폴더를 브라우징 할 수 있다. 
:::

- 모든 전송이 완료 되었을 때, 윈도우의 알림창이 뜨며, 수행 결과를 확인할 수 있다.
		- See details를 눌러 세부 수행결과를 확인한다.
<img src="/support/images/en/howto/rcloneview-basic/sync-completed-windows-alarm.png" alt="sync completed windows alarm" class="img-medium img-center" />
:::tip See the alarm messages on Windows notification
작업 완료 메시지를 놓쳤을 경우에는, 윈도우즈의 Alarm notification에서 지나간 동기화 작업 Alarm을 확인할 수 있다.
<img src="/support/images/en/howto/rcloneview-basic/click-windows-alarm-notification.png" alt="click windows alarm notification" class="img-small img-left" />
:::


## Sync 시뮬레이션을 위해 Dry run 수행하기
- Dry run을 수행한다. (Optional Operation)
	- 실제 싱크를 수행하기전에 어떤 파일들이 Destination으로 복사되고, Destination의 어떤 파일들이 삭제되는지를 시뮬레이션 한다.
	- See details를 눌러 Destination에서 발생하는 세부 operation(copy, create, delete 등) 시뮬레이션 결과를 확인할 수 있다.
<div class="img-grid-2">
<img src="/support/images/en/howto/rcloneview-basic/sync-dry-run.png" alt="sync dry run" class="img-medium img-center" />
<img src="/support/images/en/howto/rcloneview-basic/sync-dry-run-details.png" alt="sync dry run details" class="img-medium img-center" />
</div>
## 자주사용하는 Sync 오프레이션을 Jobs에 저장하기.

- 자주 수행하는 Sync 일 경우에는 Save to Jobs를 클릭하여, Job으로 저장한 후 나중에 동일한 Operation을 Job Manager를 이용하여 손쉽게 반복 수행할 수 있다. 
	- Plus 라이선스를 등록한 사용자는 Job에 대한 Scheduling 기능을 사용할 수 있다. 

<img src="/support/images/en/howto/rcloneview-basic/save-sync-to-jobs.png" alt="save sync to jobs" class="img-medium img-center" />
