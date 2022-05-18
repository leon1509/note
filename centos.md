#### CentOS7 设置开机默认不启动图形界面
````
systemctl set-default multi-user.target   -- 命令行方式启动
systemctl set-default graphical.target    -- 图形方式启动
````
以上两条命令均需要root权限执行。执行完毕后重启操作系统即可。

#### CentOS7 防火墙开放端口
````
1. 永久的开放需要的端口
   firewall-cmd --zone=public --add-port=3000/tcp --permanent
   firewall-cmd --reload
2. 检查新的防火墙规则
   firewall-cmd --list-all
````

#### CentOS7永久关闭防火墙
````
//临时关闭防火墙,重启后会重新自动打开
systemctl restart firewalld
//检查防火墙状态
firewall-cmd --state
firewall-cmd --list-all
//Disable firewall
systemctl disable firewalld
systemctl stop firewalld
systemctl status firewalld
//Enable firewall
systemctl enable firewalld
systemctl start firewalld
systemctl status firewalld
````

#### CentOS8开放端口
````
查看防火墙某个端口是否开放

firewall-cmd --query-port=3306/tcp

开放防火墙端口3306

firewall-cmd --zone=public --add-port=3306/tcp --permanent

注意：开放端口后要重启防火墙生效

重启防火墙

systemctl restart firewalld

关闭防火墙端口

firewall-cmd --remove-port=3306/tcp --permanent

查看防火墙状态

systemctl status firewalld

关闭防火墙

systemctl stop firewalld

打开防火墙

systemctl start firewalld

开放一段端口

firewall-cmd --zone=public --add-port=40000-45000/tcp --permanent

查看开放的端口列表

firewall-cmd --zone=public --list-ports

查看被监听(Listen)的端口

netstat -lntp

检查端口被哪个进程占用

netstat -lnp|grep 3306
````
