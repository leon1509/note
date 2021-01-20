````
1. 通常情况下使用varchar(20)和varchar(255)占用的空间都是一样的,但是使用索引长度有所不同。使用变长字段需要额外增加2个字节，使用NULL需要额外增加1个字节，因此对于是索引的字段，最好使用定长和NOT NULL定义，提高性能
2. 表字段的类型其实是有长度限制，int类型最大为255等等。一个表，所有字段的长度加起来不能超过65535字节，是字节不是字符 。不包括text blob类型的字段。
````

### Centos8安装MySQL5.7（已应用到vultr服务器）
    参考：https://www.cnblogs.com/sanduzxcvbnm/p/13418417.html
         https://zhuanlan.zhihu.com/p/60605885
````
1. 添加MySQL存储库
   sudo dnf remove @mysql
   sudo dnf module reset mysql && sudo dnf module disable mysql

2. centos8没有MySQL存储库，因此我们将使用centos 7存储库。创建一个新的存储库文件
   sudo vim /etc/yum.repos.d/mysql-community.repo
   内容为：
   ###### 
   [mysql57-community]
   name=MySQL 5.7 Community Server
   baseurl=http://repo.mysql.com/yum/mysql-5.7-community/el/7/$basearch/
   enabled=1
   gpgcheck=0

   [mysql-connectors-community]
   name=MySQL Connectors Community
   baseurl=http://repo.mysql.com/yum/mysql-connectors-community/el/7/$basearch/
   enabled=1
   gpgcheck=0

   [mysql-tools-community]
   name=MySQL Tools Community
   baseurl=http://repo.mysql.com/yum/mysql-tools-community/el/7/$basearch/
   enabled=1
   gpgcheck=0
   ######

3. 安装MySQL(这里选择MySQL5.7)
   sudo dnf --enablerepo=mysql57-community install mysql-community-server

4. 下载完成后检查版本
   rpm -qi mysql-community-server

5. 检查 mysql 源是否安装成功
   yum repolist enabled | grep "mysql.*-community.*"

6. 启动MySQL
   systemctl start mysqld

7. 查看启动状态
   systemctl status mysqld

8. 设置开机启动
   systemctl enable mysqld

9. 刷新所有修改过的配置文件
   systemctl daemon-reload

10. 获取安装mysql后生成的临时密码，用于登录
    grep 'temporary password' /var/log/mysqld.log

11. 登录MySQL
    mysql -uroot -p    回车后输入上面显示的密码

12. 修改登录密码
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';  -- 修改后的密码，注意必须包含大小写字母数字以及特殊字符并且长度不能少于8位,否则会报错

13. 设置默认编码为utf-8（mysql安装后默认不支持中文）
    vim /etc/my.cnf

    # 进入文件后添加下面的配置即可
    [mysqld]
    character-set-server=utf8
    collation-server=utf8_general_ci
    skip-character-set-client-handshake
    init_connect='SET NAMES utf8'

    [client]
    default-character-set=utf8

    [mysql]
    default-character-set=utf8

14. 重启MySQL服务并进入MySQL
    shell> systemctl restart mysqld
    shell> mysql -uroot -p
    mysql> show variables like 'character%';

    说明：出现以下则说明编码修改完成
    +--------------------------+----------------------------+
    | Variable_name | Value |
    +--------------------------+----------------------------+
    | character_set_client | utf8 |
    | character_set_connection | utf8 |
    | character_set_database | utf8 |
    | character_set_filesystem | binary |
    | character_set_results | utf8 |
    | character_set_server | utf8 |
    | character_set_system | utf8 |
    | character_sets_dir | /usr/share/mysql/charsets/ |
    +--------------------------+----------------------------+

````
