### 1. 下载Docker redis，并启动
```
   下载：docker pull redis
   启动：docker run -p 6379:6379 --name redis -d redis redis-server --appendonly yes
   查看容器输出：docker logs 容器ID
   查看最新前5个容器：docker ps -n 5
   再次执行容器：docker start 容器ID
   查看容器详细信息：docker inspect 容器ID
   进入一个已经运行的容器：docker exec -it 容器ID /bin/bash
```
### 2. 设置Redis密码
```
   redis-cli -h xxx.xxx.xxx.xxx -p 6379
   config set requirepass 密码
```
### 3. SpringBoot Developer Tools与热部署
```
   引入依赖：
   <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
   </dependency>

Idea设置：
   3.1 File --> Settings --> Compiler --> Build Project automatically
   3.2 勾选此项：ctrl + shift + alt + / --> Registry --> Compiler autoMake allow when app running
```
````
java -Dfile.encoding=UTF-8 -jar swc-fileserver2.war --server.port=6079 --spring.profiles.active=test

本地：
java -Xdebug -Xrunjdwp:transport=dt_socket,address=6666,server=y,suspend=n -Dfile.encoding=UTF-8 -jar -Xms256m -Xmx512m -Xmn256m swc-fileserver.war --server.port=6079 --spring.profiles.active=local

10.1.100.172：
java -Xdebug -Xrunjdwp:transport=dt_socket,address=6666,server=y,suspend=n -Dfile.encoding=UTF-8 -jar -Xms256m -Xmx512m -Xmn256m swc-fileserver3.war --server.port=6079 --spring.profiles.active=beta
````
