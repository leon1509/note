### 1. 下载Docker redis，并启动
```
   下载：docker pull redis
   启动：docker run -p 6379:6379 --name redis -d redis redis-server --appendonly yes
        或启动 5.0.10
        docker pull redis:5.0.10
        docker run -p 16379:6379 --name redis5.0.10 -d redis:5.0.10 redis-server --appendonly yes
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
### 4. 运行war和jar
````
java -Dfile.encoding=UTF-8 -jar swc-fileserver2.war --server.port=6079 --spring.profiles.active=test

本地：
java -Xdebug -Xrunjdwp:transport=dt_socket,address=6666,server=y,suspend=n -Dfile.encoding=UTF-8 -jar -Xms256m -Xmx512m -Xmn256m swc-fileserver.war --server.port=6079 --spring.profiles.active=local

10.1.100.172：
java -Xdebug -Xrunjdwp:transport=dt_socket,address=6666,server=y,suspend=n -Dfile.encoding=UTF-8 -jar -Xms256m -Xmx512m -Xmn256m swc-fileserver3.war --server.port=6079 --spring.profiles.active=beta
````
### 5. Docker启动ElasticSearch
````
1. 拉取ES镜像
   docker pull elasticsearch
2. 创建交接模式网络
   docker network create es_network
3. 运行ES容器
   docker run -d --name es1 -p 9200:9200 -p 9300:9300 --network es_network -v /d/work/es_volume:/root -e "privileged=true" -e "discovery.type=single-node" elasticsearch
````
参数说明：
|参数|参数说明|
|:--|:--|
|-d|后台运行|
|--name  es1|容器名称|
|-p 9200:9200 -p 9300:9300|映射端口（宿主端口:容器端口）|
|--network es_network|指定承载网络|
|-v /d/work/es_volume:/root|共享目录映射（宿主目录:容器目录）|
|-e "privileged=true"|配置访问权限|
|-e "discovery.type=single-node"|指定ElasticSearch部署模式|
|elasticsearch|指定派生的镜像|

### 6. 框架集成库
````
Mysql、
Oracle、
SQLServer、
PostgreSQL、
TiDB（同Mysql）
ElasticSearch、
HBase、
Lombok、
Hibernate-validator、
Redis、
MongoDB、
Hutool、
MinIO、
Knife4j（Swagger）、
Mybatis-plus、
logback、
RabbitMQ、
Activiti、
多数据源

- 单独搭建：
MinIO
XXL-job
api网关
ELK
开源代码质量管理平台：sonarqub
TiDB
CodeGenerator
RabbitMQ
监控（prometheus）
````

### 7. Docker安装PostgreSQL
````
拉取镜像：docker pull postgres
启动镜像：docker run --name mypostgres -d -p 5432:5432 -e POSTGRES_PASSWORD=123456 postgres
进入容器：docker exec -it mypostgres psql -U postgres -d postgres
使用终端命令连接：psql -U username -h ipaddress -d dbname
查看数据库所有表：select * from pg_tables;
````
### 8. Docker安装Oracle 12c
````
拉取镜像：docker pull truevoly/oracle-12c
启动镜像：docker run --name oracle12c -d -p 8088:8080 -p 1521:1521 -v /f/oracle/data:u01/app/oracle truevoly/oracle-12c
         说明：启动并暴露8088：8080&1521：1521端口，并且挂载宿主机目录 /f/oracle/data 到oracle容器的/u01/app/oracle 目录
进入容器：docker exec -it oracle12c /bin/bash
         su - oracle
         sqlplus / as sysdba
         GRANT CONNECT,RESOURCE,DBA TO ora_test IDENTIFIED 123456;
````
### 9. 部署顶级项目pom到私服
````
cls&& mvn deploy:deploy-file -Dfile=wrd-ma-spring-boot-parent-1.1.3.pom -DgroupId=cn.piesat.wrd -DartifactId=wrd-ma-spring-boot-pare
nt -Dversion=1.1.3 -Dpackaging=pom -Durl=http://10.1.4.130:8081/repository/wrd-framework/ -DrepositoryId=wrd-framework

注意：
      9.1 pom文件不要放在本地仓库.m2中，否则上面的命令将执行失败。
      9.2 setting.xml文件<servers>部分要加入：
      <server>
         <id>wrd-framework</id>
         <username>admin</username>
         <password>xxxxxx</password>
      </server>
      
````
