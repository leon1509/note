```
1. Docker环境下秒建Redis集群，连SpringBoot也整上了！ >>> http://www.macrozheng.com/#/reference/redis_cluster
2. 从中央仓库拉取镜像，重新打上tag，并上传到私服（私服地址10.1.4.130:8083）：
   2.1 拉取centos7镜像： docker pull centos:7
   2.2 打标签： docker tag centos:7 10.1.4.130:8083/centos:7
   2.3 上传到私服： docker push 10.1.4.130:8083/centos:7

```
