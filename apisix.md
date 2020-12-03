Docker安装apisix：
- 下载最新版etcd镜像3.4.14：docker pull bitnami/etcd
- 下载最新版apisix 2.1：docker pull apache/apisix
- 创建docker网络：docker network create --driver=bridge --subnet=172.18.0.0/16 --ip-range=172.18.5.0/24 --gateway=172.18.5.254 apisix
- 启动etcd服务器：docker run -it --name etcd-server -v /d/Work/docker-instance/apisix-docker/example/etcd_conf/etcd.conf.yml:/opt/bitnami/etcd/conf/etcd.conf.yml -p 2379:2379 -p 2380:2380 --network apisix --ip 172.18.5.10 --env ALLOW_NONE_AUTHENTICATION=yes bitnami/etcd
- 启动apisix服务器：docker run --name apisix -v /d/Work/docker-instance/apisix-docker/example/apisix_conf/config.yaml:/usr/local/apisix/conf/config.yaml -v /d/Work/docker-instance/apisix-docker/example/apisix_log:/usr/local/apisix/logs -p 9080:9080 -p 9443:9443 --network apisix --ip 172.18.5.11 -d apache/apisix

参考：https://github.com/apache/apisix-docker/blob/master/manual.md
