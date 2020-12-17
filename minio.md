windows docker环境下安装minio：
````
1. 下载minio镜像：docker pull minio/minio
2. 运行minio镜像，并将MiniIO的数据和配置文件夹挂在到宿主机：
   docker run -p 9000:9000 --name minio1 -v F:\data:/data -e "MINIO_ACCESS_KEY=AKIAIOSFODNN7EXAMPLE" -e "MINIO_SECRET_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY" minio/minio server /data
````
