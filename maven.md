注意： pom中的dependencyManagement节点作用是：只是对版本进行管理，不会实际引入jar ！！！

```
mvn dependency:sources 重新下载项目中依赖的jar包。
```
1. 跳过Javadoc
```
   -Dmaven.javadoc.skip=true
```
---------------------------------
2. 本地jar/pom包安装到远程仓库
```
   mvn deploy:deploy-file -DgroupId=com.oracle -DartifactId=ojdbc14 -Dversion=11.2.0.4.0 -Dpackaging=jar -Dfile=D:\oracleDB\product\11.2.0\dbhome_1\jdbc\lib\ojdbc6.jar -Durl=http://10.1.4.130:8081/repository/wrd-framework/ -DrepositoryId=wrd-framework
   mvn deploy:deploy-file -Dfile=xx.pom -DgroupId=com.nero.www -DartifactId=demo -Dversion=0.1.0 -Dpackaging=pom -Durl=http://10.1.4.130:8081/repository/wrd-framework/ -DrepositoryId=wrd-framework
```
   其中：
groupId，artifactId，version 是maven中jar包的坐标信息，packaging指定包类型，file指定jar包文件的位置，url指定发布到nexus私服上的路径，可以在nexus web管理界面copy，repositoryId是仓库名。
注意：需要配置Nexus认证信息，在本机的maven的配置文件conf.xml中配置 nexus 认证信息：
```
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
```
注意ID要和nexus中配置的仓库唯一名称保持一致
--------------------------------------
3. 本地jar/pom包安装到本地.m2仓库
```
mvn install:install-file -Dfile=ojdbc8-12.2.0.1.jar -DgroupId=com.oracle -DartifactId=ojdbc8 -Dversion=12.2.0.1 -Dpackaging=jar
   mvn install:install-file -Dfile=xx.pom -DgroupId=com.nero.www -DartifactId=demo -Dversion=0.1.0 -Dpackaging=pom
```
4. 关于向Nexus私服上传jar/pom失败的问题
   安装第三方jar到Artifact, 从Artifact的官方上看到其实有很多种方法(请看这里),最简单的就是从Archiva的web 页面上找到Upload Artifact这个功能。
   使用maven的 deploy:deploy-file 命令时要注意的是：如果要安装的jar和pom是位于本地repository的目录下，这个命令就会出错 (Cannot deploy artifact from the local repository…), 
   解决方法：将要安装的jar和pom 复制到其它目录再安装，只要不在本地仓库目录就可以。

5. 使用maven打包的时候，会发现外部jar包没打包进依赖，需要在pom.xml进行资源添加：
```
   <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.7.0</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <goals>
                            <goal>repackage</goal><!--可以把依赖的包都打包到生成的Jar包中-->
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
        <resources>
            <resource>
                <directory>lib</directory>
                <targetPath>BOOT-INF/lib/</targetPath>
                <includes>
                    <include>**/*.jar</include>
                </includes>
            </resource>
        </resources>
    </build>
```
    参考： https://www.cnblogs.com/GuixinChan/p/13164294.html
