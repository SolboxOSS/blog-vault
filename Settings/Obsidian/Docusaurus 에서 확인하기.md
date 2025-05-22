
## Docusaurus Github Repository

https://github.com/SolboxOSS/rcloneview-support.git


## Obsidian 의 .md 파일과 첨부파일(이미지) 복사하기

- Obsidian 폴더에 대응하는 Docusaurus 폴더로 .md 파일과 첨부파일을 복사. ^ece3e8

|         구분          | Obsidian 폴더                | Docusaurus 폴더             | 설명                               |
| :-----------------: | :------------------------- | :------------------------ | :------------------------------- |
|     .md or .mdx     | /en/howto                  | /howto                    | - help guide(매뉴얼) 문서 작성 폴더       |
|     .md or .mdx     | /en/tutorials              | /tutorials                | - Tutorial 문서 작성 폴더              |
| html 문법 첨부파일(이미지 등) | /support/images/[md파일 폴더명] | /static/images/[md파일 폴더명] | - .md 파일내에 첨부된 파일(이미지 등) 저장 폴더   |
|   md, mdx 문법 첨부파일   | /en/[md파일폴더]/attachments   | /[md파일폴더]/attatchments    | - .md, .mdx와 함께 첨부파일 폴더 그대로 복사하기 |
|                     |                            |                           |                                  |
- 이미지의 폴더는 아래와 같이 매핑 됩니다.  ^841efb
	- ⚠️ html 문법을 이용한 image 의 경우 Docusaurus의 Webpack 이 관여하지 않으므로 반드시 /static/images/로 복사를 해야하며, .md, .mdx 에서 링크를 최종 rcloneview.com 도메인의 절대경로와 동일하게 지정해야 합니다. (💡html 방식은 이미지 리사이징, 정렬에 유리)
	- ✅ Markdwon 이나 JSX 문법을 이용한 image의 경우 상대경로 지정시 Docusaurus의 Webpack이 html 을 생성하면서 이미지 경로를 자동으로 매핑하므로 Obsidian과 Dousaurus의 폴더구조를 그대로 유지하면 됩니다. ( 💡 상대경로가 가독성이 좋으므로 상대경로를 사용. )
	- 💡단, JSX 문법을 사용하면 이미지 리사이징, 정렬을 하면서 동시에 상대경로를 사용할 수 있습니다. 

| 구분                     | Obsidian(Source)     | Docusaurus(Source)   | Docusaurus (Build)    | rcloneview.com          |
| ---------------------- | -------------------- | -------------------- | --------------------- | ----------------------- |
| html 문법 images         | /support/images/     | /static/images/      | /build/images/        | /support/images/        |
| Markdown, JSX 문법images | [현재폴더]/attatchments/ | [현재폴더]/attatchments/ | /build/assets/images/ | /support/assets/images/ |
   
## Docusaurus로 Build 및 실행하기

- 아래의 명령을 순차적으로 실행
```bash
rm -rf .docusaurus/ build/
npm run build             
npm run start
```

- 브라우저에서  http://localhost:3000/support/ 로 접속하여 확인.

