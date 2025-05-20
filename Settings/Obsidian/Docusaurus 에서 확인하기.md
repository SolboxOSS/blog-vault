
## Docusaurus Github Repository

https://github.com/SolboxOSS/rcloneview-support.git


## Obsidian 의 .md 파일과 첨부파일(이미지) 복사하기

- Obsidian 폴더에 대응하는 Docusaurus 폴더로 .md 파일과 첨부파일을 복사.

|         구분          | Obsidian 폴더                | Docusaurus 폴더             | 설명                             |
| :-----------------: | :------------------------- | :------------------------ | :----------------------------- |
|         .md         | /en/howto                  | /howto                    | - help guide(매뉴얼) 문서 작성 폴더     |
|         .md         | /en/tutorials              | /tutorials                | - Tutorial 문서 작성 폴더            |
| html 문법 첨부파일(이미지 등) | /support/images/[md파일 폴더명] | /static/images/[md파일 폴더명] | - .md 파일내에 첨부된 파일(이미지 등) 저장 폴더 |
|     md 문법 첨부파일      | /en/howto/attachments      | /howto/attatchments       | - .md와 함께 첨부파일 폴더 그대로 복사하기     |
|                     |                            |                           |                                |

## Docusaurus로 Build 및 실행하기

- 아래의 명령을 순차적으로 실행
```bash
rm -rf .docusaurus/ build/
npm run build             
npm run start
```

- 브라우저에서  http://localhost:3000/support/ 로 접속하여 확인.

