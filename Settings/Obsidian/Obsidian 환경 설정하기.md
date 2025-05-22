
## ✅ Github 저장소

https://github.com/SolboxOSS/blog-vault.git

## ✅ 여러 개의 문서 프로젝트(Vault) 관리 방법

 Obsidian에서는 “Vault(금고)“라는 개념을 사용하여 하나의 문서 프로젝트 단위를 관리합니다. 여러 개의 문서 프로젝트를 생성하고 싶다면, **Vault를 여러 개 만드는 것**이 가장 기본적인 방법입니다. 

https://obsidian.md/download

## ✅ 필수 플러그인 설치

### 플러그인 활성화

Obsidian 좌측 하단 Settings(⚙️) →
**Community plugins** → **Turn on Safe Mode** → **Browse** 버튼 클릭

### TailwindCSS 실시간 적용하기위한 플러그인 설치
#####  📌 Style Settings 플러그인 설치

- 이름: **Style Settings**
- 설명: Custom CSS를 쉽게 적용하고 관리할 수 있게 해줍니다.

**설치 방법:**

- “Style Settings” 검색 → 설치 → Enable
  ![[img/Pasted image 20250430144626.png]]

#### 📌 Minimal Theme Settings 플러그인 설치 (선택사항)

- 더 강력한 Tailwind 연동 테마를 원하면 “Minimal Theme”를 추가합니다.
- Obsidian 기본 테마만으로도 가능하지만, Minimal Theme는 Tailwind를 적용하기에 더 깔끔합니다.

**설치 방법:**
- Obsidian 좌측 하단 Settings(⚙️) →
- **Community plugins** →  **Browse** 버튼 클릭
- “Minimal Theme Settings” 검색 → 설치 → Enable
  ![[img/Pasted image 20250430144732.png]]

#### ❗TailwindCSS Custom Styles 적용

  1. Obsidian Vault 루트의  .obsidian/snippets/ 아래에 ~.css 파일 생성 혹은 저장. ![[img/obsidian.css]]
2. Obsidian Settings → Appearance → **CSS Snippets**에서 활성화

![[img/Pasted image 20250506000919.png]]

**(예시)**

```markdown

<div class="p-4 bg-blue-500 text-center text-white rounded-lg">
  Hello, Tailwind in Obsidian!
</div>
```

> [!success] 
> 아래와 같이 파란 바탕색에 흰색 글자가 보이면 제대로 적용 된 것임. 

<div class="p-4 bg-blue-500 text-center text-white rounded-lg">
  Hello, Tailwind in Obsidian!
</div>

### 📌 Templater 플러그인 설치

**설치 방법:**
- Obsidian 좌측 하단 Settings(⚙️) →
- **Community plugins** →  **Browse** 버튼 클릭
- “Templater” 검색 → 설치 → Enable



**❗Templater 환경 변수 설정**

- Obsidian 좌측 하단 Settings(⚙️) →
-  Templater 선택 -> 
	- 📋 Templater folder location :  templater
	- 🔍 Template hotkeys : templater/auto-Front-matter.md
		- 🔗 '+' 버튼 눌러서 hotkey 설정: 예) cmd(ctrl) + F
	- 🛠️ **User system command functions** > Enable user system command fucnditons:  ✅ 

❗**Hotkeys 추가**
- Obsidian 좌측 하단 Settings(⚙️) →
-  Hotkeys 선택 -> Templater: Open insert template modal -> 예) cmd(ctrl) + T 설정.

> [!tip] 
> 나중에 아래와 같이 template 모달창을 통해 Template를 불러서 사용하기 위함.  
> 
> ![](Settings/Obsidian/attachments/Pasted%20image%2020250520142625.png)


### 📌 Manual sorting 플러그인 (권장사항)

Obsidian의 사이드바 Tree에서 페이지 순서를 수동으로 바꿀수 있게해주는 플러그인.
필수는 아니나 설치하면 편리함.


### Markdown Cheat Sheet 플러그인 (선택사항)

1. **설정 → Community plugins → Browse** 로 이동
    
2. Markdown Format Assistant  검색 후 설치
   ![[img/Pasted image 20250430142536.png]]

3. 포맷을 클릭만으로 삽입 가능하며, Markdown 문법을 빠르게 복습할 수 있음

> [!tip] 
> 특히, Callouts를 이용하면, 현재의 Tip 박스와 같이 다양한 인포메이션 박스 템플릿을 사용할 수 있음. 


### 🧩 깨진 링크 확인: Broken Links Plugin (선택사항)
![](attachments/Pasted%20image%2020250521231557.png)

## ✅ Obsidian Settings 변경

**📋 Appearance > Show inline title 설정 **
- File name을 최상단에 위치하는 것으로 H1과 혼동의 여지가 있으므로 'Off' 해두는 것이 좋음.

![](attachments/Pasted%20image%2020250523005012.png)

**📋 Files and links 설정 **

🔗 Settings(⚙️) > Files & Links 메뉴로 이동
1. New link format 을 'Relative path to file' 로 설정.
2. Use [wikilkinks]를 비활성화.
3. Default location for new attatchments 를 'In subfolder under current folder' 로 설정. ^af5b5b
4. Subfolder name 을 'attatchments' 로 설정.

![](attachments/Pasted%20image%2020250520175414.png)
> [!danger] 
> - Docusaurus에 html 문법을 이용해  삽입하는 이미지는 Templater의 clipboard-html-image-insert 템플릿을 통해 저장하여야 함. 
> - 이 템플릿을 이용하여 저장하는 이미지는 /support/images/[현재폴더이름]/  아래에 자동 저장되며, Docusaurus의 /static/images/[현재폴더이름]/ 에 그대로 복사하여 사용함.
> 🔗 [Obsidian 의 .md 파일과 첨부파일(이미지) 복사하기](Docusaurus%20에서%20확인하기.md#Obsidian%20의%20.md%20파일과%20첨부파일(이미지)%20복사하기)



## ✅ Obsidian으로 Tech blog Template 사용 (선택사항)

1. **Settings(⚙️) > Template 메뉴로 이동**
2. template 폴더 지정

![[img/Pasted image 20250502175335.png]]

> [!info] 
>  template 폴더와 폴더 내에 미리 자주 사용하는 템플릿을 .md 파일로 만들어 두세요.

> [!tip] 
> ![[img/Pasted image 20250505210815.png]] 
> Hot key 로 등록해두면 편함.
> 



