---
sidebar_position: "1"
id: quick-start-guide
title: Quick Start Guide
slug: /howto/quick-start-guide
description: Quick start guide to use RcloneView.
keywords:
  - rclone
  - cloud
  - sync
  - rcloneview
  - guide
tags:
  - RcloneView
  - Cloud
  - Sync
date: <% tp.date.now("YYYY-MM-DD") %>
author: Jay
---

# Quick Start Guide

## RcloneView 설치

[RcloneView homepage](https://rcloneview.com/src/download.html) 에서 설치파일을 다운로드 후 프로그램 설치를 완료
하세요. 
:::note
설치시에 license agreement에 동의하셔야 합니다. 
![](/support/images/Pasted%20image%2020250506191753.png)
:::

설치완료 후 아래의 화면이 보이실 겁니다. 

## 원격 스토리지 추가

다음으로 구글 드라이브를 추가해 보겠습니다. 

:::note
새로운 Remote를 추가하기 전에 구글 드라이브 계정을 미리 만들어 두시길 바랍니다. 
:::

화면의 오른쪽 창에서 '+' 버튼을 눌러서 remote 추가 창을 뛰웁니다.

- Markdown image insert test
![](/support/images/Pasted%20image%2020250508144524.png)

- html image insert test
<img src="/support/images/Pasted%20image%2020250508144524.png" alt="large image" width="auto" class="img-small" />
<div class="img-grid-2">
  <img src="/support/images/Pasted%20image%2020250508144524.png" alt="이미지1" />
  <img src="/support/images/Pasted%20image%2020250508144524.png" alt="이미지2" />
</div>



검색창에서 'google' 을 검색한 후 'Google Drive'를 선택합니다. 

![](img/Pasted%20image%2020250508154442.png)

다음 화면은 입력을 하지 않고 스킵합니다. 
![](img/Pasted%20image%2020250508160223.png)

  
     
:::note 참고
Google 등 SSO(Sing Sign On)를 지원하는 클라우드 스토리지들은 Options을 그냥 스킵하시면 SSO 인증 후 연결이 완료 됩니다.
Google Drive와 같이 SSO 방식의 접속을 지원하는 클라우드 스토리지는 Dropbox, Google photos, Microsoft Onedrive, Box, pCloud, Yandex Disk, premiumize.me, put.io,HiDrive 등이 있습니다.
SSO를 지원하는 클라우드 스토리지 중 Options 항목 입력이 필요한 Zoho WorkDrive, Google Cloud Storage, Citrix ShareFile, Google Drive Shared with me, Box for Business 는 다음 링크를 참조하셔서 설정하시길 바랍니다. 
:::

추가하는 드라이브에 대한 이름을 지정 합니다. 
![](img/Pasted%20image%2020250508160259.png)

저장 버튼을 눌러 리모트 추가를 완료 합니다. 
![](img/Pasted%20image%2020250508160511.png)

:::note 참고
'*' 로 표시된 필수 입력사항을 입력하지 않았을 경우 'save' 가 불가능하며, 안내 메시지에 따라 입력을 완료하신 후 'Save'를 완료하시면 됩니다.
:::

## 원격 스토리지 계정 연결 - SSO:Single Sign On 방식

구글 SSO 로그인 사이트로 이동됩니다. 
기존에 저장되어 있는 구글 계정을 선택합니다.
![](img/Pasted%20image%2020250508163942.png)

혹은, 'Use another account'를 선택하여 구글 계정으로 로그인을 시도 합니다.
![](img/Pasted%20image%2020250508164017.png)
![](img/Pasted%20image%2020250508163753.png)


미리 설정해둔 로그인 방법을 이용하여 로그인을 완료 합니다. 


![](img/Pasted%20image%2020250508164537.png)

:::note 참고
위의 Password 방식이 아닌 다른 방식으로 로그인을 하실 경우 다음의 링크를 참조하시어 진행을 완료하시길 바랍니다. https://support.google.com/accounts/answer/12849458 
:::

다음 continue를 눌러 구글드라이버 연결을 완료 합니다. 

![](img/Pasted%20image%2020250508170238.png)

아래의 화면이 보이면 성공적으로 구글 드라이브 연결이 완료 되었습니다. 

![](img/Pasted%20image%2020250508170443.png)

자 이제부터 RcloneView를 이용한 구글드라이브의 파일 관리와 동기화를 즐기실 준비가 완료 되었습니다. 

## 다음 학습하기.

- 다양한 원격 스토리지 연결
- RcloneView을 이용한 기본 파일 관리
- RcloneView를 이용한 파일 동기화

RcloneView를 이용한 기본 파일 관리.
RcloneView를 이용한 파일 동기화.

## 📎 Related documents (관련 문서)

- 👉[기초 설치 가이드](app://obsidian.md/tutorials/install-guide)
- 👉[고급 동기화 팁](app://obsidian.md/guides/advanced-sync)

