# 用單一 function 來部屬好像野蠻有趣的
[link](https://cloud.google.com/functions/docs/quickstart#functions-prepare-environment-go)

# prepare
- 啟用 Cloud Functions and Cloud Build API
- 安裝並更新 gcloud，設定預設專案
- 先複製 helloworld 專案
- 部屬 gcloud function，目前 gcloud function 環境只能用 go113，設定區域會比較好
```shell
gcloud functions deploy HelloGet \
  --region asia-east1 \
  --runtime go113 --trigger-http --allow-unauthenticated
```
- 在部屬的過程中，可以先去 cloud build 看 log
- 用 describe 拿 gcloud 的路徑(httpsTrigger)
```shell
gcloud functions describe HelloGet
```
- delete function
```shell
gcloud functions delete HelloGet 
```

# 類型:怎開始寫
[link](https://cloud.google.com/functions/docs/writing)
- 主要有兩種 triger 方式 http function 及 event function
- http function寫法([link](https://cloud.google.com/functions/docs/writing/http))
- event function寫法([link](https://cloud.google.com/functions/docs/writing/background))
- src code 架構禁止以 package main 作為名字，會希望以以下架構存放
```shell
.
├── function.go
├── go.mod
└── shared/
    └── shared.go
```
- 可以使用 [Functions Framework](https://github.com/GoogleCloudPlatform/functions-framework-go) 進行 local 測試，沒問題後再進行部屬
