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
