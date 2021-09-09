### MacOS 将大文件压缩为指定大小的多个小文件，例：

````
zip - openjdk-16.0.2_windows-x64_bin.zip | split -b 25600k - openjdk-16.0.2.zip.
说明：
25600k表示压缩后每个小文件的尺寸，25600k=25M
最后面的是压缩后的文件前缀，命令执行完后会在后面自动添加aa、ab、ac。。。。

在windows中将上面压缩后的小文件解压，首先将后缀aa这些改为001、002。。。。然后用压缩软件解压即可。
````

### ARM架构的 apple M1 安装 Homebrew 和 Homebrew cask
````
切换shell到bash

安装Homebrew： /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
安装Homebrew cask： 
  1. brew install homebrew/cask-version
  2. brew install homebrew/cask
  3. brew install caskroom/cask/brew-cask
  以上三个命令都执行一遍（不知道哪个有效）
````
````
[安装多版本的JDK](https://github.com/leon1509/note/blob/master/jdk.md '安装多版本的JDK')
````

### Mac从其它渠道接收的文件，权限部分带有Finder标签@符号，如何去除？

````
使用xattr命令：
查看文件接收渠道：xattr -l 目录[文件]
去除文件Finder标签：xattr -c 文件[目录]
去除目录及子目录/文件下的所有Finder标签：xattr -cr 目录/
````
