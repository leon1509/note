```
1. Docker环境下秒建Redis集群，连SpringBoot也整上了！ >>> http://www.macrozheng.com/#/reference/redis_cluster
2. 从中央仓库拉取镜像，重新打上tag，并上传到私服（私服地址10.1.4.130:8083）：
   2.1 拉取centos7镜像： docker pull centos:7
   2.2 登录私服： docker login -u admin -p 密码 10.1.4.130:8083
   2.3 打标签： docker tag centos:7 10.1.4.130:8083/centos:7
   2.4 上传到私服： docker push 10.1.4.130:8083/centos:7
3. 牛逼！Docker从入门到上瘾： https://mp.weixin.qq.com/s/1whzKVnL2hLwViNRVh7f5Q

```
