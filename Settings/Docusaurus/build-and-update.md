# Build 후에 작업

1. /build/ 폴더 -> rcloneview.com/support 로 복사.
2. Typesense scraper 로 인덱싱 업데이트
	run the scraper (rcloneview-support 에서 실행)
```bash
docker run -it --env-file=/Users/gimjuhong/.env -e "CONFIG=$(cat config.json | jq -r tostring)" typesense/docsearch-scraper:0.11.0


```
3. Bing, Google, Naver Sitemap 업데이트 요청.

4. IndexNow API로 Bing 인덱싱, Naver 인덱싱 요청. (자주하면 안됨, 모아서 한꺼번에... )

```Bind Indexing Request


```




