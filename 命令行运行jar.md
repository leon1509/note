````
java -Xms256m -Xmx512m -Dserver.port=9000 -jar -Dlogging.file=/var/logs/xxxx.log xxxx.jar --spring.config.location=application-prod.yml &
````

#### SpringBoot业务jar包与依赖jar包分离部署，实现jar包优化瘦身
````
方法一：
    1. 在pom.xml中加入以下代码：
    <build>
      <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <includes>
                    <!-- 不存在的include引用，相当于排除所有maven依赖jar，没有任何三方jar文件打入输出jar -->
                    <include>
                        <groupId>null</groupId>
                        <artifactId>null</artifactId>
                    </include>
                </includes>
                <layout>ZIP</layout>
            </configuration>
            <executions>
                <execution>
                    <goals>
                        <goal>repackage</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
      </plugins>
    </build>
    
    加入以上代码后，mvn package后生成的jar包不包括依赖jar。
    
    2. 单独将依赖的jar库生成到指定目录
    mvn dependency:copy-dependencies -DoutputDirectory=target/lib -DincludeScope=compile
    
    此命令会将工程所依赖的jar库copy到工程目录下的lib里面
    
    3. 运行业务jar包
    java -jar -Djava.ext.dirs=lib sso-admin-1.8.jar --spring.profiles.active=prod
    
    这样，当业务代码有更新时，只需将第1步生成的瘦身后的业务jar包更新至服务器即可。
    
    注意：当有新依赖库加入时，记得将第2步重新生成。
    
方法二：
    将【方法一】中的第1、2步都放到IDE中一步生成。参考：https://mp.weixin.qq.com/s/GpqWXKYT4M1qAmzcryKLGQ
````
