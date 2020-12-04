Docker安装apisix：

#### 1. 拉取镜像及Dashboard源码
- 下载最新版etcd镜像3.4.14：docker pull bitnami/etcd
- 下载最新版apisix 2.1：docker pull apache/apisix
- 拉取apisix-docker源码：git clone https://github.com/apache/apisix-docker.git
- 拉取apisix-dashboard源码：git clone https://github.com/apache/apisix-dashboard.git && cd apisix-dashboard

#### 2. 创建docker网络：docker network create --driver=bridge --subnet=172.18.0.0/16 --ip-range=172.18.5.0/24 --gateway=172.18.5.254 apisix

#### 3. 运行etcd服务器：
   PS：下面命令中的etcd.conf.yml文件是上面下载的apisix-docker项目中的文件
````
   docker run -d --name etcd-server -v /d/Work/docker-instance/apisix-docker/example/etcd_conf/etcd.conf.yml:/opt/bitnami/etcd/conf/etcd.conf.yml -p 2379:2379 -p 2380:2380 --network apisix --ip 172.18.5.10 --env ALLOW_NONE_AUTHENTICATION=yes 10.1.4.130:8083/bitnami/etcd:3.4.14
````

#### 4. 运行apisix服务器：
   PS：下面命令中的config.yaml文件、apisix_log目录是上面下载的apisix-docker项目中的文件
````
   docker run --name apisix -v /d/Work/docker-instance/apisix-docker/example/apisix_conf/config.yaml:/usr/local/apisix/conf/config.yaml -v /d/Work/docker-instance/apisix-docker/example/apisix_log:/usr/local/apisix/logs -p 9080:9080 -p 9443:9443 --network apisix --ip 172.18.5.11 -d 10.1.4.130:8083/apache/apisix:2.1
````

#### 5. 构建并运行apisix-dashboard镜像：
   - 修改源码目录下的的Dockfile： 将所有ARG ENABLE_PROXY=false 改为：ARG ENABLE_PROXY=true
   或者构建的时候添加下面--build-arg参数：
   ````
   docker build -t apisix-dashboard:2.1.1 . --build-arg ENABLE_PROXY=true
   ````

   - 构建dashboard镜像：docker build -t apisix-dashboard:2.1.1 .

   - 修改apisix-dashboard/api/conf/conf.yaml中etcd服务器IP地址等信息，
   - 启动dashboard： 
   ````
   docker run -d -p 9500:9500 -v /d/Work/docker-instance/apisix-dashboard/api/conf/conf.yaml:/usr/local/apisix-dashboard/conf/conf.yaml --name apisix-dashboard --network apisix --ip 172.18.5.12 apisix-dashboard:2.1.1
   ````

   - 访问dashboard： http://10.1.14.130:9500 admin/admin

 参考：
 	- https://github.com/apache/apisix-dashboard/blob/v2.1.1/docs/deploy-with-docker.zh-CN.md

