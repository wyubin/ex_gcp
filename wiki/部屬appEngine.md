# intro
將程式布到 app engine

# 部屬在 App Engine
## ref
[link](https://cloud.google.com/go/getting-started#deploying-your-app-to-app-engine)

- 主要使用 app.yaml 來設定，一樣是用 cloud shell
  - deploy
  ```shell
  cd ~/cloudshell_open/golang-samples/getting-started/bookshelf
  # 當然要已經設定跑在 gcloud config set project eminent-hall-320902
  # 這步驟要跑一陣子
  gcloud app deploy
  # 通常這步驟可能要試幾次 [link](https://stackoverflow.com/questions/66528149/deploying-django-on-google-app-engine-error-gcloud-app-deploy-not-found)
  ```
- 接下來就可以去 [link](https://eminent-hall-320902.de.r.appspot.com) 操作
- 再來去 firestore 去找存好的資料。
- 可以參考 [link](https://cloud.google.com/firestore/docs/manage-data/add-data#go) 在程式中做操作

# 在 Cloud Storage 中存储上传的文件
- 先進到 Cloud Storage 建立一個分區(通常是 [projectid]_bucket)
  - 要注意權限要設定精細權限
- 進入分區並設定公開權限 [link](https://cloud.google.com/storage/docs/access-public-data)
- 到 app 選擇修改圖書並上傳照片，就會把找片存到 Cloud Storage
- 程式的操作方法如 [link](https://github.com/GoogleCloudPlatform/golang-samples/blob/HEAD/getting-started/bookshelf/main.go#L189-L230)
- 回到那個 bucket 就可以看到圖擋了

# 使用 Google Cloud 的运维套件监控您的应用
- 在 app 中轉到 /logs 來建立 log
- 轉到 loggings 來看 log 列表，主要是在 GAE application

# 使用 Error Reporting 监控错误
- 一樣用 /errors 來建立測試 error
- 就可以到 error reporter 就看狀況
- 可以打開到 panic 去看出問題的程式碼行數

# 心得
- 用 GAE 部屬 app，藉由 firestore 取代資料庫(nosql)的部份，再藉著 Cloud Storage 存靜態檔
- 如果是要開發一個會使用 google 服務或是一個免費應用，可以考慮用這種方式