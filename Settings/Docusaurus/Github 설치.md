
Docusaurus 프로젝트를 GitHub에 저장하려면 다음 단계를 따라 진행하면 됩니다:

---

## **✅ 1. GitHub 저장소 만들기**

1. [https://github.com](https://github.com) 접속
    
2. 오른쪽 상단 “+” → **New repository** 클릭
    
3. 저장소 이름 입력 (예: rcloneview-support)
    
4. **Public** 또는 **Private** 선택
    
5. README 초기화는 _체크 안 함_ (로컬에서 Push할 것이므로)
    
6. **Create repository**
    

---

## **✅ 2. 로컬 프로젝트 Git에 연결**

  

터미널에서 Docusaurus 프로젝트 폴더로 이동:

```
cd /path/to/your-docusaurus-project
```

Git 초기화 및 커밋:

```
git init
git add .
git commit -m "Initial commit"
```

원격 저장소 연결:

```
git remote add origin https://github.com/사용자명/저장소명.git
```

예시:

```
git remote add origin https://github.com/SolboxOSS/rcloneview-support.git
```

  

---

## **✅ 3. GitHub에 Push**

```
git branch -M main
git push -u origin main
```

> [!error]
>  ```bash
> gimjuhong@Mac rcloneview-support % git push -u origin main
Username for 'https://github.com': jay@solbox.com
Password for 'https://jay@solbox.com@github.com': 
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
fatal: Authentication failed for 'https://github.com/SolboxOSS/rcloneview-support.git/' 


## **✅ GitHub SSH 인증 설정 (Mac 기준)**

  

### **🔹 1. SSH 키 생성**

  

터미널에 아래 명령어 입력:

```
ssh-keygen -t ed25519 -C "jay@solbox.com"
```

출력 예:

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/gimjuhong/.ssh/id_ed25519): [엔터]
Enter passphrase (empty for no passphrase): [엔터]
```

> ~/.ssh/id_ed25519 (개인키), ~/.ssh/id_ed25519.pub (공개키) 생성됨

---

### **🔹 2. SSH 에이전트 실행 및 키 등록**

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

  

---

### **🔹 3. 공개키 GitHub에 등록**

  

공개키 내용 복사:

```
cat ~/.ssh/id_ed25519.pub
```

출력된 키를 복사한 후, 아래 경로 접속:

  

🔗 [https://github.com/settings/keys](https://github.com/settings/keys)

→ “New SSH key” 클릭

→ **Title**: MacBook SSH 등

→ **Key**에 붙여넣기

→ **Add SSH key**

---

### **🔹 4. 원격 URL SSH 방식으로 변경**

```
git remote set-url origin git@github.com:SolboxOSS/rcloneview-support.git
```

확인:

```
git remote -v
```

결과:

```
origin  git@github.com:SolboxOSS/rcloneview-support.git (fetch)
origin  git@github.com:SolboxOSS/rcloneview-support.git (push)
```

  

---

### **🔹 5. Push 실행**

```
git push -u origin main
```

  

---

## **✅ 참고: SSH 연결 테스트**

```
ssh -T git@github.com
```

정상 출력 예:

```
Hi SolboxOSS! You've successfully authenticated, but GitHub does not provide shell access.
```

  

---

이제 SSH로 GitHub에 안전하게 푸시할 수 있습니다.

SSH 키를 다른 컴퓨터에도 설정하고 싶다면 id_ed25519와 id_ed25519.pub를 복사해가면 됩니다.

  




