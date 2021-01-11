```
1. 跳过Javadoc
   -Dmaven.javadoc.skip=true
---------------------------------
2. 本地jar包安装到远程仓库
   mvn deploy:deploy-file -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=11.2.0.4.0 -Dpackaging=jar -Dfile=D:\oracleDB\product\11.2.0\dbhome_1\jdbc\lib\ojdbc6.jar -Durl=http://localhost:8081/repository/maven-3rd-party/ -DrepositoryId=nexus-3rd-party

   配置本地maven的confg.xml配置文件：

   <servers>
      <server>
         <id>maven-public</id>
         <username>admin</username>
         <password>xxxx</password>
      </server>
      <server>
         <id>nexus-3rd-party</id>
         <username>admin</username>
         <password>xxxx</password>
      </server>
   </servers>

注意ID要和nexus中配置的仓库唯一名称保持一致
--------------------------------------
3. 本地jar包安装到本地.m2仓库
   mvn install:install-file -Dfile=ojdbc8-12.2.0.1.jar -DgroupId=com.oracle -DartifactId=ojdbc8 -Dversion=12.2.0.1 -Dpackaging=jar
```
