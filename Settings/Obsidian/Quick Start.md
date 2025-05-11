

# 여러 개의 문서 프로젝트(Vault) 생성 방법

 Obsidian에서는 “Vault(금고)“라는 개념을 사용하여 하나의 문서 프로젝트 단위를 관리합니다. 여러 개의 문서 프로젝트를 생성하고 싶다면, **Vault를 여러 개 만드는 것**이 가장 기본적인 방법입니다. 

## 새로운 Vault 생성

1. Obsidian 실행
    
2. 시작 화면에서 **“Create new vault”** 클릭
    
3. 아래 항목 입력
    
    - **Vault name**: 프로젝트 이름
        
    - **Vault location**: 해당 프로젝트 폴더가 저장될 경로
        
    
4. **“Create”** 클릭
    

   이로써 완전히 독립된 프로젝트 환경이 구성됩니다.

# Markdown Cheat Sheet 플러그인 사용

1. **설정 → Community plugins → Browse** 로 이동
    
2. Markdown Format Assistant  검색 후 설치
   ![[img/Pasted image 20250430142536.png]]

3. 포맷을 클릭만으로 삽입 가능하며, Markdown 문법을 빠르게 복습할 수 있음

> [!tip] 
> 특히, Callouts를 이용하면, 현재의 Tip 박스와 같이 다양한 인포메이션 박스 템플릿을 사용할 수 있음. 

![[img/Pasted image 20250502182725.png]]


# Obsidian으로 Tech blog Template 사용

1. **Settings(⚙️) > Template 메뉴로 이동**
2. template 폴더 지정

![[img/Pasted image 20250502175335.png]]

> [!info] 
>  template 폴더와 폴더 내에 미리 자주 사용하는 템플릿을 .md 파일로 만들어 두세요.

> [!tip] 
> ![[img/Pasted image 20250505210815.png]] 
> Hot key 로 등록해두면 편함.
> 


# Images 폴더 관리 방법

## 🎯 목표

- Obsidian에서 이미지를 붙여넣으면 해당 폴더의 ./img 에 저장
- Docusaurus로 이동시, 해당 폴더 전체를 copy & past 적용.

> [!note] 
> 아래와 같이 vault의 특정폴더(Obsidian)에 .md 파일을 작성시(Quick Start.md) 해당 폴더내에 img 폴더를 생성해서 작성하고, 작업 완료 후 해당 폴더 전체를 docusaurus로 옮기면 됨.
> 
> ![[img/Pasted image 20250502184615.png]]
> 


## Obsidian Settings 변경**

1. **Settings(⚙️) > Files & Links 메뉴로 이동**
2. New link format 을 'Relative path to file' 로 설정.
3. Default location for new attatchments 를 'In subfolder under current folder' 로 설정.
4. Subfolder name 을 'img' 로 설정.

![[img/Pasted image 20250502165129.png]]


## 이미지 링크 표준 .md 스타일로 저장하도록 수정.
* Files and links 에서 Use [[wikilkinks]] 를 비활성화.
![](img/Pasted%20image%2020250506002845.png)


# Obsidian에서 TailwindCSS 실시간 적용하는 방법


## 플러그인 활성화

  

Obsidian 좌측 하단 Settings(⚙️) →

**Community plugins** → **Turn on Safe Mode** → **Browse** 버튼 클릭

## 꼭 설치해야 할 플러그인 2개

### Style Settings

- 이름: **Style Settings**
    
- 설명: Custom CSS를 쉽게 적용하고 관리할 수 있게 해줍니다.
    

**설치 방법:**

- “Style Settings” 검색 → 설치 → Enable
  ![[img/Pasted image 20250430144626.png]]

### Minimal Theme Settings (선택사항)

- 더 강력한 Tailwind 연동 테마를 원하면 “Minimal Theme”를 추가합니다.
    
- Obsidian 기본 테마만으로도 가능하지만, Minimal Theme는 Tailwind를 적용하기에 더 깔끔합니다.

**설치 방법:**

- “Minimal Theme Settings” 검색 → 설치 → Enable
  ![[img/Pasted image 20250430144732.png]]

### TailwindCSS Custom Styles 적용

  

1. Obsidian Vault 루트의  .obsidian/snippets/ 아래에 obsidian.css 파일 생성 혹은 저장. ![[img/obsidian.css]]
2. Obsidian Settings → Appearance → **CSS Snippets**에서 활성화
3. Markdown 문서 안에서 Tailwind 유틸리티 클래스 사용!

![[img/Pasted image 20250506000919.png]]

###  **예시**

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


# 링크깨진 파일 관리 방법

**🧩 추천 커뮤니티 플러그인: Dangling Links Plugin**

![[img/Pasted image 20250502170202.png]]

## 마크다운 문법의 이미지 링크 적용하기. 
![](support/images/Pasted%20image%2020250511233844.png)