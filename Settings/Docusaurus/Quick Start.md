
## Fast Track ⏱️[​](https://docusaurus.io/docs#fast-track "Direct link to Fast Track ⏱️")

Understand Docusaurus in **5 minutes** by playing!

Create a new Docusaurus site and follow the **very short** embedded tutorial.

Install [Node.js](https://nodejs.org/en/download/) and create a new Docusaurus site:

```
npx create-docusaurus@latest my-website classic
```

Start the site:

```Bash
cd my-website 
npx docusaurus start
```

or
```bash
cd my-website
npm run build
npm run serve

```

Open [`http://localhost:3000`](http://localhost:3000/) and follow the tutorial.

## [[Github 설치]]



## Base URL을 /Support/로 변경

1. docusaurus.config.js 의 baseUrl: '/' 를 '/support/' 로 변경.


2. 

## Tailwind css 설치



## Static Site Generation and RcloneView 홈페이지 Support 페이지 복수 절차.

1. Static Site Generation !

```bash
npm run build
```

2. Docusaurus /build/ 폴더를 RcloneView /support/ 폴더로 복사.
3. RcloneView /Support/의 index.html에 RcloneView header Bar code 추가.




## Obsidian과 공동 사용 CSS 설정.
  

### **🔹 1. Obsidian의 CSS 추출**

  

Obsidian 테마(기본 또는 커스텀)는 보통 vault/.obsidian/snippets/ 에 있습니다
```css obsidian style
/* Images */

.markdown-preview-view img {

// border-top: 4px solid #3b82f6;

border-radius: 8px;

box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);

padding: 0.2rem;

background-color: white;

display: block;

margin: 1.5rem auto;

max-width: 100%;

height: auto;

transition: transform 0.2s ease;

}

.markdown-preview-view img:hover {

transform: scale(1.03);

}

/* Captions */

.markdown-preview-view figure {

text-align: center;

margin: 1rem auto;

}

.markdown-preview-view figcaption {

font-size: 0.85rem;

color: #6b7280;

margin-top: 0.25rem;

}
```

Docusaurus의 테마에 맞도록 수정.

```css
/* 이미지에 스타일 적용 */
.theme-doc-markdown img {
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  padding: 0.2rem;
  background-color: white;
  display: block;
  margin: 1.5rem auto;
  max-width: 100%;
  height: auto;
  transition: transform 0.2s ease;
}
.theme-doc-markdown img:hover {
  transform: scale(1.03);
}

/* 캡션 스타일 */
.theme-doc-markdown figure {
  text-align: center;
  margin: 1rem auto;
}
.theme-doc-markdown figcaption {
  font-size: 0.85rem;
  color: #6b7280;
  margin-top: 0.25rem;
}
```


  

### **1. CSS 파일 위치 변경 (혹은 복사)**

  
```
src/css/obsidian-docusaurus-theme.css
```

> 💡 src/css/ 폴더는 Docusaurus에서 Webpack으로 번들링되며 가장 안정적으로 스타일이 적용됩니다.

---

### **2.** **docusaurus.config.js**


```
theme: {
  customCss: [
    './src/css/custom.css',
    './src/css/obsidian-docusaurus-theme.css',  // ← ✅ 여기 추가
  ],
},
```

> 기존의 custom.css에 추가 배열 형식으로 지정 가능

---

