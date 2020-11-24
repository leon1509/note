```
1. 下载Docker redis，并启动
   下载：docker pull redis
   启动：docker run -p 6379:6379 --name redis -d redis redis-server --appendonly yes
   查看容器输出：docker logs 容器ID
   查看最新前5个容器：docker ps -n 5
   再次执行容器：docker start 容器ID
```
