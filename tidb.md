### 1. tidb服务器断电后pd无法启动，使用pd-recover故障恢复
参考：https://win-man.github.io/2020/06/16/051-pd-recovery/
````
1. 集群版本：5.1.0
2. 故障现象：TiDB集群的物理机异常断电重启,机器恢复后,通过 tiup cluster start <cluster-name> 启动集群，发现 PD 节点启动失败

3. 故障解决步骤：
    3.1 参考官方文档 PD Recover 使用文档 ,通过 pd-recovery 工具恢复集群。
        根据文档内容主要分为 3 个步骤：
        1. 找到 cluster id 
        2. 找到当前最大 alloc id 
        3. 通过 pd-recovery 恢复 pd 集群
    3.2 下载pd-recover工具：参见https://docs.pingcap.com/zh/tidb/stable/pd-recover#pd-recover-%E4%BD%BF%E7%94%A8%E6%96%87%E6%A1%A3
    3.3 故障恢复
        /* 查找cluster id */
        # cat /home/tidb-deploy/pd-2379/log/pd.log | grep "init cluster id"
        
        /* 查找当前最大的 alloc id （因为 pd-recovery 去恢复的时候需要指定一个比当前最大的 alloc id 更大的 alloc id，所以需要对所有的 pd 节点日志进行查找）
           如果因误删除了pd日志文件，直接采用较大的数作为alloc id（本次恢复就用此方法，使用10000作为alloc id）
        */
        # cat /home/tidb-deploy/pd-2379/log/pd.log | grep "allocates"
        
        /*
        删除旧 PD 集群 data 目录下的所有内容
        */
        # mv /home/tidb-data/pd-2379/* /tmp/backup/tidb/pd-data (事先建好此目录)
        
        /*
        启动 PD 集群
        */
        # tiup cluster start tidb-test -R pd
        
        /*
        使用pd-recover恢复集群
        */
        # pd-recover -endpoints http://10.1.5.73:2379 -cluster-id 6823755660393880966 -alloc-id 10000
        
        /*
        重启 PD 集群
        */
        # tiup cluster restart tidb-test -R pd
        
        /*
        启动tidb集群
        */
        # tiup cluster start tidb-test
        
        /*
        查看集群状态，已恢复正常
        */
        # tiup cluster display tidb-test
````
