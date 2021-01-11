```
1. 跳过Javadoc
   -Dmaven.javadoc.skip=true
---------------------------------
2. 本地jar包安装到远程仓库
   mvn deploy:deploy-file -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=11.2.0.4.0 -Dpackaging=jar -Dfile=D:\oracleDB\product\11.2.0\dbhome_1\jdbc\lib\ojdbc6.jar -Durl=http://localhost:8081/repository/maven-3rd-party/ -DrepositoryId=nexus-3rd-party
   
   其中：
groupId，artifactId，version 是maven中jar包的坐标信息，packaging指定包类型，file指定jar包文件的位置，url指定发布到nexus私服上的路径，可以在nexus web管理界面copy，repositoryId是仓库名。
注意：需要配置Nexus认证信息，在本机的maven的配置文件conf.xml中配置 nexus 认证信息：
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
