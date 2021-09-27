# 1. 内网yum私服


为应对在政务或其它内网使用Linux部署系统不便，特编写此教程。

----

一、准备一台笔记本电脑，硬盘至少200G+。

    安装与生产环境相同版本的CentOS操作系统。
    同时安装nginx、httpd或python环境中至少一种（一般情况下，系统自带python，如果没有安装，请单独安装）。


二、首先将该笔记本电脑连接公网，在最大挂载的盘下创建目录（命名随意，本教程假设为/home/yumdata）。


三、使用yum（如果系统中没有该命令需要自行安装）安装相关组件，示例如下（以下#号开头的行为注释）：

````
    # 安装createrepo和reposync组件
    $  yum install createrepo reposync
    # 注意：如果安装过程中，出现如下提示：
    `
    No package reposync available.
    Nothing to do
    `
    # 解决方法为：安装 yum-utils，命令如下：
    $ yum install yum-utils
````
---
四、创建yum软件包资源库

````
    $  cd /home/yumdata
    # 1. 下载 base 目录包
    $ reposync --repoid=base
    # 2. 下载 updates 目录包
    $ reposync --repoid=updates
    # 3. 下载 extras 目录包
    $ reposync --repoid=extras
    # 4. 下载 epel 目录包
    $ reposync --repoid=epel
    # 以上下载yum软件包资源库时间较长，因此该项工作需要提前做好。
````
---
五、生成yum软件包资源库源（元）数据

````
    $ cd /home/yumdata
    # 1. 生成base目录软件包源（元）数据
    $ createrepo --update base/
    # 2. 生成updates目录软件包源（元）数据
    $ createrepo --update updates/
    # 3. 生成extras目录软件包源（元）数据
    $ createrepo --update extras/
    # 4. 生成epel目录软件包源（元）数据
    $ createrepo --update epel/
````
---
六、启动http文件浏览服务

   方便起见，本示例采用python作为http服务器（nginx和apache httpd请自行参考网上教程）。
````
    $  cd /home/yumdata
    # 在80端口，以/home/yumdata为服务根目录，启动http服务
    $  python3 -m http.server 80
````
   效果见下图：
   ![20210927144700.jpg](/uploads/projects/wrd_dev_spec/16a89af51487ee03.jpg "20210927144700.jpg")
 PS：请忽略端口号

---

七、配置内网部署项目的服务器

  7.1. 环境要求：

   1. 部署项目的服务器操作系统需与上面的笔记本电脑操作系统版本一致
  
   2. 部署项目的服务器需安装有yum，如果没有可下载安装离线版
   
   3. 将上面的笔记本电脑接入部署项目服务器所在相同的内网

7.2 修改部署用服务器的yum源为上述的私服（即笔记本电脑）

约定：

   - 约定1：本节所示的命令中，##开头的是以root身份执行的命令，非注释行。一个#号的还是注释
   - 约定2：本节假定笔记本电脑的IP为192.168.1.10，http服务运行在80端口，即yum软件包资源库的URL为：http://192.168.1.10/
   - 编辑yum配置文件

````
    # 以root用户身份登录或使用sudo（本示例以root身份讲解）
    ## cd /etc/yum.repos.d/
    # 创建bak目录，并将当前目录下的所有文件移至bak目录中
    ## mkdir bak
    ## mv .repo* bak
    # 再将bak目录下的CentOS-Base.repo复制到当前目录进行编辑
    ## cp bak/CentOS-Base.repo .
    # 编辑CentOS-Base.repo文件内容
    ## vim CentOS-Base.repo
````
内容如下：

````
[base]
name=CentOS-$releasever - Base - wrd.piesat.cn
failovermethod=priority
baseurl=http://192.168.1.10/base/
release=$releasever&arch=$basearch&repo=os
gpgcheck=0
enabled=1
#gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
 
#released updates 
[updates]
name=CentOS-$releasever - Updates - wrd.piesat.cn
failovermethod=priority
baseurl=http://192.168.1.10/updates/
release=$releasever&arch=$basearch&repo=updates
gpgcheck=0
#gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
 
#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras - wrd.piesat.cn
failovermethod=priority
baseurl=http://192.168.1.10/extras/
release=$releasever&arch=$basearch&repo=extras
gpgcheck=0
#gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus - wrd.piesat.cn
baseurl=http://192.168.1.10/extras/
release=$releasever&arch=$basearch&repo=epel
gpgcheck=0
enabled=1
#gpgkey=http://mirrors.aliyun.com/centos/RPM-GPG-KEY-CentOS-7
````

- 清理已有缓存并重新生成

````
   ## yum clean all
   ## yum makecache
````
- 安装项目依赖需要的软件

````
   ## yum install xxxxx
````

八、写在最后

** 因没有实际内网环境做测试、所以以上流程为理论流程。如在部署过程中有任何问题，请及时沟通。**

# 2. 待续
