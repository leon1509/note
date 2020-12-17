windows docker环境下安装minio：
````
1. 下载minio镜像：docker pull minio/minio
2. 运行minio镜像，并将MiniIO的数据和配置文件夹挂在到宿主机：
   docker run -p 9090:9090 --name minio -v /f/data/minio:/data -v /f/data/minio/config:/root/.minio -d minio/minio server /data
````
