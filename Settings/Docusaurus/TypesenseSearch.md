## Typesense Server 설치

ssh -i "statsapi.pem" ubuntu@ec2-18-117-197-178.us-east-2.compute.amazonaws.com


https://typesense.org/docs/guide/install-typesense.html#linux-binary

```bash
curl -O https://dl.typesense.org/releases/28.0/typesense-server-28.0-linux-amd64.tar.gz
tar -xzf typesense-server-28.0-linux-amd64.tar.gz
```

### 실행

```bash
mkdir data

./typesense-server --data-dir=./data --api-key=greatercloneview1! --listen-port=8108 --enable-cors
```

### 자동실행 설정
#### **1) 서비스 유닛 파일 생성**

```
sudo vi /etc/systemd/system/typesense-server.service
```


```
[Unit]
Description=Typesense Server
After=network.target

[Service]
Type=simple
WorkingDirectory=/home/ubuntu
ExecStart=/home/ubuntu/typesense-server --data-dir=/home/ubuntu/data --api-key=greatercloneview1! --listen-port=8108 --listen-host=0.0.0.0 --cors
User=ubuntu
Restart=always
RestartSec=3
StandardOutput=append:/home/ubuntu/typesense-server.log
StandardError=append:/home/ubuntu/typesense-server.log

[Install]
WantedBy=multi-user.target
```

#### **3) 적용 및 자동시작 등록**
```
sudo systemctl daemon-reload
sudo systemctl enable typesense-server
sudo systemctl start typesense-server

## 정상 실행상태 확인: 

sudo systemctl status typesense-server
```

### AWS 보안 설정
8108 inbound 허용

### 접속 확인


- 서버 정상 실행 시

http://ec2-18-117-197-178.us-east-2.compute.amazonaws.com:8108/health → {"ok":true}

## Typesense Scaraper 설치


https://github.com/typesense/typesense-docsearch-scraper



### step1. config.json 작성

https://github.com/algolia/docsearch-configs/blob/master/configs/docusaurus-2.json

```config.json
{
  "index_name": "docusaurus-2",
  "start_urls": [
    "http://rn.solbox.com/support"
  ],
  "sitemap_urls": [
    "http://rn.solbox.com/support/sitemap.xml"
  ],
  "sitemap_alternate_links": true,
  "stop_urls": [

  ],
  "selectors": {
    "lvl0": {
      "selector": "(//ul[contains(@class,'menu__list')]//a[contains(@class, 'menu__link menu__link--sublist menu__link--active')]/text() | //nav[contains(@class, 'navbar')]//a[contains(@class, 'navbar__link--active')]/text())[last()]",
      "type": "xpath",
      "global": true,
      "default_value": "Documentation"
    },
    "lvl1": "header h1",
    "lvl2": "article h2",
    "lvl3": "article h3",
    "lvl4": "article h4",
    "lvl5": "article h5, article td:first-child",
    "lvl6": "article h6",
    "text": "article p, article li, article td:last-child"
  },
  "strip_chars": " .,;:#",
  "custom_settings": {
    "separatorsToIndex": "_",
    "attributesForFaceting": [
      "language",
      "version",
      "type",
      "docusaurus_tag"
    ],
    "attributesToRetrieve": [
      "hierarchy",
      "content",
      "anchor",
      "url",
      "url_without_anchor",
      "type"
    ]
  },
  "conversation_id": [
    "833762294"
  ],
  "nb_hits": 46250
}

```

### Step2. Scraper  실행

install docker
install jq
make .env

```
TYPESENSE_API_KEY=greatercloneview1!
TYPESENSE_HOST=typesense.rcloneview.com
TYPESENSE_PORT=443
TYPESENSE_PROTOCOL=https
```

```
TYPESENSE_API_KEY=greatercloneview1!
TYPESENSE_HOST=ec2-18-117-197-178.us-east-2.compute.amazonaws.com
TYPESENSE_PORT=8108
TYPESENSE_PROTOCOL=http
```

run the scraper (rcloneview-support 에서 실행)
```bash
docker run -it --env-file=/Users/gimjuhong/.env -e "CONFIG=$(cat config.json | jq -r tostring)" typesense/docsearch-scraper:0.11.0


```

오류 시 대응.

```
curl -X DELETE 'http://ec2-18-117-197-178.us-east-2.compute.amazonaws.com:8108/collections/docs' -H 'X-TYPESENSE-API-KEY: greatercloneview1!'

curl -X DELETE 'http://ec2-18-117-197-178.us-east-2.compute.amazonaws.com:8108/aliases/docs' -H 'X-TYPESENSE-API-KEY: greatercloneview1!'
```



npm install typesense typesense-instantsearch-adapter react-instantsearch-dom


Error 발생시 package.json 에서 Reqct version 교체 후

``` package.json
"react": "^18.3.0",
"react-dom": "^18.3.0",
```

npm 재 설치
```
rm -rf node_modules package-lock.json  
npm install
```


### Typesense Search Box 설치

npm install @docusaurus/plugin-sitemap --save

- Https로 설정.
- 홈페이지가 https로 운영되므로, 반드시 Typesense 서버 앞단에 Proxy를 설치해서 https로 접속되게해야함.

```docusaurus.config.js

themeConfig:
  /** @type {import('@docusaurus/preset-classic').ThemeConfig} */
  ({
    // ... 기존 themeConfig 내용 ...

    typesense: {
      typesenseCollectionName: 'docs',  // 본인의 컬렉션 이름
      typesenseServerConfig: {
        nodes: [
          {
            host: 'typesense.rcloneview.com',
            port: 443,
            protocol: 'https',
          },
        ],
        apiKey: 'greatercloneview1!',
      },
      typesenseSearchParameters: {}, // 옵션
      contextualSearch: true,        // 옵션
    },

    // ... 나머지 themeConfig (footer, prism 등) ...
  }),

```


- http 개발용으로 설정

```docusaurus.config.js

themeConfig:
  /** @type {import('@docusaurus/preset-classic').ThemeConfig} */
  ({
    // ... 기존 themeConfig 내용 ...

    typesense: {
      typesenseCollectionName: 'docs',  // 본인의 컬렉션 이름
      typesenseServerConfig: {
        nodes: [
          {
            host: 'ec2-18-117-197-178.us-east-2.compute.amazonaws.com',
            port: 8108,
            protocol: 'http',
          },
        ],
        apiKey: 'greatercloneview1!',
      },
      typesenseSearchParameters: {}, // 옵션
      contextualSearch: true,        // 옵션
    },

    // ... 나머지 themeConfig (footer, prism 등) ...
  }),
```


Swizzling


### Typesense Dashboard

https://bfritscher.github.io/typesense-dashboard/


```
docker run -it --rm -p 5001:5000 bfritscher/typesense-dashboard:main

```

Docker:
https://hub.docker.com/r/bfritscher/typesense-dashboard


Github site:

https://github.com/bfritscher/typesense-dashboard