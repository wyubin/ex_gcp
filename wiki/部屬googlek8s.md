# intro
將程式布到 GKE

# ref
[link](https://cloud.google.com/kubernetes-engine/docs/quickstarts/deploying-a-language-specific-app)

# prepare
- 要啟用 Artifact Registry, Cloud Build, and Google Kubernetes Engine API
- 安裝 google cloud sdk [link](https://cloud.google.com/sdk/docs/install)
```shell
curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-347.0.0-linux-x86_64.tar.gz
tar zxvf google-cloud-sdk-347.0.0-linux-x86_64.tar.gz
./google-cloud-sdk/install.sh
./google-cloud-sdk/bin/gcloud init
```
- 再用 gcloud 指令來安裝 kubectl(通常還是要安裝 gcloud 的kubectl才能正常執行)
```shell
gcloud components install kubectl
```

# implement app image
- 在 golang 的 container 編寫好了之後，就可以在外面把 src code 傳到 k8s 上了
- 先在 artifacts 建立一個repo
```shell
gcloud artifacts repositories create hello-repo \
    --project=k8s-test-320908 \
    --repository-format=docker \
    --location=asia-east1 \
    --description="Docker repository"
```
- build image，先到 src code 位置再進行下面操作
```shell
gcloud builds submit \
    --tag asia-east1-docker.pkg.dev/k8s-test-320908/hello-repo/helloworld-gke .
```

# 创建 GKE 集群
- 先以 gcloud 部屬 helloworld images
```shell
gcloud container clusters create helloworld-gke \
    --num-nodes 1 \
    --zone asia-east1-b
```
- 以 kubectl access gcp，需要先拿憑證
```shell
gcloud container clusters get-credentials helloworld-gke
# access
kubectl get nodes
```
# 部署到 GKE
- 需要用到兩個設定檔來定義
  - deployment.yaml 用來設定 app 怎麼啟動
  - service.yaml 設定網頁如何 access
- 在 scr code 的位置建立這兩個檔案後，部屬到 gke上
```shell
# deployment
kubectl apply -f deployment.yaml
# check status
kubectl get deployments
# check pods
kubectl get pods
```
- service
```shell
# service
kubectl apply -f service.yaml
# check status
kubectl get services
# check service
http://[EXTERNAL-IP]
```

# 心得
- 依據自己希望使用的 os 及相關工具以 vm 的方式部屬到 gke 上，主要可獲得更客製化的資源及其他資源，但要組成一個完整的服務則需要更多考慮，像是資料庫等等的
