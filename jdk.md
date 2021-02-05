### Mac M1 安装多个版本的 JDK
````
1. 下载JDK
   JDK 推荐使用 zulu jdk，这个是适配 Arm 架构的 jdk，[下载地址](https://www.azul.com/downloads/zulu-community/?package=jdk "zulu JDK")
   选择.zip结尾的即可，下载后解压到不含中文的目录中。如：jdk8、jdk11、jdk15

2. 设置环境变量
   配置.bash_profile（bash）/.zshrc（zsh），内容如下：
   
   export JDK8_HOME=/Users/root/Dev/jdk/jdk8
   export JDK11_HOME=/Users/root/Dev/jdk/jdk11
   export JDK15_HOME=/Users/root/Dev/jdk/jdk15

   alias jdk8="export JAVA_HOME=$JDK8_HOME"
   alias jdk11="export JAVA_HOME=$JDK11_HOME"
   alias jdk15="export JAVA_HOME=$JDK15_HOME"

   保存退出，并执行 source ~/.bash_profile 或 source ~/.zshrc

3. 使用
   使用的时候，命令行执行：jdk8，即使用jdk1.8，其它亦如此（jdk11 或 jdk15）
````
