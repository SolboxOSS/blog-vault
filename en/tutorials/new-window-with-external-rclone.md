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
date: 2025-06-19
author: Jay
---
# Open New RcloneView Window for External Rclone

RcloneView는 다수의 Rclone Engine과 연동하여 각각 외부의 Rclone 엔진을 동작시킬 수 있습니다. 

RcloneView의 동작원리


사용자의 이해를 돕기 위해 위해 외부의 AWS 클라우드에 Rclone Engine을 운영하고, 해당 외부 Rclone과 연결하여 클라우드 파일을 관리하는 예를 들어 설명해보겠습니다.

:::important YOU NEED PLUS LICENSE TO OPEN NEW RclonView Window
You will need to purchase a [**PLUS license**](https://rcloneview.com/src/pricing.html) to enable this functionality.
:::

## AWS 클라우드 상에 Rclone Engine 구동하기.

AWS 클라우드에서 Rclone을 실행하고 외부에서 API(rclone rcd)로 접근할 수 있도록 구성하는 전체 절차는 다음과 같습니다. 이 가이드는 **Ubuntu 기반 EC2 인스턴스**를 기준으로 설명합니다.

---

## **✅ 전체 순서 요약**

1. AWS EC2 인스턴스 생성
    
2. 보안 그룹 설정 (포트 5572 열기)
    
3. SSH로 인스턴스 접속
    
4. Rclone 설치
    
5. Rclone 초기 설정 (선택 사항)
    
6. Rclone rcd 데몬 실행
    
7. 외부에서 Rclone API 접속 확인
    

---

## **1️⃣ AWS EC2 인스턴스 생성**

1. AWS Management Console 로그인
    
2. **EC2** 서비스 이동 → **인스턴스 시작 (Launch Instance)** 클릭
    
3. 설정:
    
    - **이름**: rclone-server (원하는 이름)
        
    - **AMI**: Ubuntu Server 22.04 LTS (또는 20.04 LTS)
        
    - **인스턴스 유형**: t2.micro (무료 티어 대상 가능)
        
    - **키페어**: 새로 생성하거나 기존 키 선택 (SSH 접속용)
        
    - **스토리지**: 기본 8GB 이상
        
    - **네트워크**: 기본 VPC
        
    - **보안 그룹**:
        
        - SSH (포트 22): 내 IP
            
        - **Custom TCP (포트 5572): Anywhere (0.0.0.0/0)** ← 중요
            
        
    
4. 인스턴스 시작
    

---

## **2️⃣ 보안 그룹 확인 및 수정 (필요 시)**

- EC2 > 인스턴스 > 인스턴스 선택 > 보안 탭 > 보안 그룹 클릭
    
- **인바운드 규칙 편집**
    
    - 포트 5572 열기
        
    

```
유형: Custom TCP
포트 범위: 5572
소스: 0.0.0.0/0 또는 특정 IP
```

  

---

## **3️⃣ SSH로 EC2 접속**

  

로컬 터미널에서:

```
chmod 400 /path/to/your-key.pem
ssh -i /path/to/your-key.pem ubuntu@<EC2-Public-IP>
```

---

## **4️⃣ Rclone 설치**

```
curl https://rclone.org/install.sh | sudo bash
```

설치 확인:

```
rclone version
```

---

## **5️⃣ Rclone 구성 (선택)**

```
rclone config
```

원격 저장소를 등록하거나, 필요 없다면 생략 가능.

---

## **6️⃣ Rclone rcd 실행**

```
rclone rcd \
  --rc-user=admin \
  --rc-pass=admin \
  --rc-addr=0.0.0.0:5572 \
  --rc-web-gui
```

옵션 설명:

- --rc-user, --rc-pass: 인증 정보
    
- --rc-addr=0.0.0.0:5572: 외부에서 접근 가능하도록 설정
    
- --rc-web-gui: GUI도 같이 실행하려면 사용
    

  

> **백그라운드 실행 (예: tmux나 systemd) 추천**:

```
sudo apt install tmux -y
tmux
rclone rcd --rc-user=admin --rc-pass=admin --rc-addr=0.0.0.0:5572
```

---

## **7️⃣ 외부에서 API 접속 테스트**

  

브라우저 또는 Postman에서:

```
http://<EC2-Public-IP>:5572/core/version
```

- 인증 필요 → Basic Auth: admin / admin
    

---

## **🛡️ 보안 권장 사항**

- 실제 운영환경에서는 rc-user, rc-pass를 복잡한 값으로 설정하세요.
    
- IP 제한 (예: --rc-addr=YOUR_PUBLIC_IP:5572) 또는 AWS 보안 그룹으로 제한
    
- HTTPS 사용은 프록시(Nginx, Cloudflare Tunnel 등) 통해 구현 가능
    





## RcloneView의 New Window로 외부 Rclone Engine 연결하기.

본 시나리오는 RcloneView Main Window는 Embedded Rclone과 연결하여 운영을 하고, 새로운 RcloneView 윈도우를 외부 Rclone 과 연결하여 사용하는 것을 가정한 사용 시나리오 입니다. 


