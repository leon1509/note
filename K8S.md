### 1. 在K8S+Kubesphere安装Redis集群
参考：https://github.com/bitnami/charts/blob/master/bitnami/redis-cluster/README.md
```
# helm repo add bitnami https://charts.bitnami.com/bitnami
// redis-cluster 服务名称（随便自定义）
# helm install redis-cluster --set password=Qwe#321 bitnami/redis-cluster -n wrd-gansu-shanhong

-- 删除Redis集群
# helm delete redis-cluster
```

### 2. 
