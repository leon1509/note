### 在windows7上安装docker和hbase镜像和hadoop镜像
- https://www.dazhuanlan.com/2019/09/23/5d881d00c7833/

````
    docker pull harisekhon/hbase

    docker run -d -h myhbase -p 2181:2181 -p 8080:8080 -p 8085:8085 -p 9090:9090 -p 9095:9095 -p 16000:16000 -p 16010:16010 -p 16020:16020 -p 16030:16030 --name hbase2.x.x harisekhon/hbase
    -d: 后台启动。
    -h: 容器主机名，必须设置该项并配置 hosts，否则无法连通容器。
    -p: 网络端口映射，这里只把要使用的端口（zookeeper端口、HBase Master端口、HBase RegionServer端口等）映射了出来，你可以根据自己需要进行端口映射。
    –name: 容器别名。

    添加说明：大多数的博客贴在进行到这里的时候都是映射端口为16201和16301，没有16020和16030。经过查看 http://192.168.99.100:16010/master-status 页面，发现安装的最新hbase2.1.1版本，
    默认启动的是16020和16030。这里特别注意

    进入hbase命令行
    docker exec -it hbase1.3.1 /bin/bash
    /hbase/bin/hbase shell
    hbase(main):001:0> create 't1', {NAME => 'f1', VERSIONS => 1}

    在执行完第一个命令进入hbase容器后，可以执行netstat -anp | grep 16000 来查看hbase绑定的

    ip 172.17.0.2
    1 Created table t1
    2 Took 2.6696 seconds
    3 => Hbase::Table - t1
````
