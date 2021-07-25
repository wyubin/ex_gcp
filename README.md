# intro
練習如何使用 GCP 部屬 go app

# ref
[Go 使用入门](https://cloud.google.com/go/getting-started)

# note
## 準備
[link](https://cloud.google.com/go/getting-started)
- 建立新帳號: 設定好信用卡就可以開使用了
- 從首頁先選擇專案，再從側邊選 fitestore 的 資料就可以確定模式
  - 選原生模式
  - 位置選台灣後就可以建立資料庫
- 啟用 App Engine Admin, Cloud Storage, Cloud Logging, and Error Reporting API
  - 先從首頁確定哪些沒開之後，再去 api 打開
  - App Engine Admin 如果設定是應用程式使用，就可以不用憑證
- 進到cloud shell 來進行 golang example 的設定
  - 找到 project id 並設定授權
  ```shell
  gcloud config set project eminent-hall-320902
  ```
## run app
- build
```shell
go build
```
- 把程式跑在設定的 project 上面的 8080
```shell
GOOGLE_CLOUD_PROJECT=eminent-hall-320902 ./bookshelf
```
- 按網頁總覽(右上方)就可以