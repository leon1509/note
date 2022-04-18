# gitlib常用操作

Command line instructions

Git global setup
````
git config --global user.name "中文名"
git config --global user.email "xxxx@xxxx.com.cn"
````

Create a new repository
````
git clone ssh://git@git.xxxx.cn:7022/xxxx/project.git
cd pie_hydr_alg
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
````

Existing folder
````
cd existing_folder
git init
git remote add origin ssh://git@git.xxxx.cn:7022/xxxx/project.git
git add .
git commit -m "Initial commit"
git push -u origin master
````

（接上）修改文件或目录内容再传：
````
git add .
git commit -m "注释"
git push
````

Existing Git repository
````
cd existing_repo
git remote rename origin old-origin
git remote add origin ssh://git@git.xxxx.cn:7022/xxxx/project.git
git push -u origin --all
git push -u origin --tags
````

# 忽略.DS_Store文件，并删除已经上传的.DS_Store文件

全局设置忽略
虽然每个项目配.gitignore文件可以成功，但是每个项目都需要配，嗯，有点烦。我们可以在git的全局进行配置来忽略.DS_Store文件。

设置之前我们先看下现在的git config配置情况（git config官方文档说明）：
````
$ git config --list
````
实际上git配置情况可以在 ~/.gitconfig 文件中查看。
````
$ vi ~/.gitconfig
````
通过 :q! 退出后，我们需要建立一个文件，把需要全局忽略的文件路径写入其中。该文件起名为.gitignore_global：

````
$ touch ~/.gitignore_global
````
然后对这个文件进行修改。

````
# Mac OS
**/.DS_Store
````
然后对git进行全局设置，让git忽略.gitignore_global中的所有文件：
````
$ git config --global core.excludesfile ~/.gitignore_global
````
这样就不用每个git目录都设置忽略.DS_Store文件了！

删除已经上传到仓库里的.DS_Store文件：
描述：gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。

解决方法就是先把本地缓存删除（改变成未track状态），然后再提交:
````
git rm -r --cached .
git add .
git commit -m "删除.DS_Store"
git push
````


------ 以下为旧的经验，只供参考 -------

### 1. 删除项目与git的关联关系（Idea 2020.3版本）
````
  1.1 Idea中，项目右键-->Git-->Manage Remotes，减号删除项目与git的关联关系。
  1.2 进入项目目录，删除.git目录
  1.3 Idea中，File-->Settings-->Version Control，减号删除右边的关联关系。(windows)
      Idea中，IntelliJ IDEA --> Preferences --> Version Control，减号删除右边的关联关系。(MacOS)
````

### 2. 删除gitlab或github上的多余目录
````
  2.1 拉取项目到本地（如果本地已存在，则略过）
      $ git clone xxxxxxx 或 git pull origin master

  2.2 在本地仓库删除文件
      $ git rm 文件

  2.3 在本地仓库删除target文件夹 -r表示递归所有子目录
      $ git rm -r --cached target

  2.4 提交代码
      $ git commit -m '删除xx目录'

  2.5 推送到远程仓库
      $ git push origin master（或xxxxxxx）
````

### 3. 使用 git 提交多个项目到同一个仓库中（https://www.pianshen.com/article/97731377065/）
````
1. 在要提交的目录上点击右键 -> Git Bash Here
2. 在打开的终端依次输入：
   2.1 git init	// 初始化仓库，项目出现绿色打钩图标，并且生成.git文件夹
   2.2 git remote add origin ssh://git@git.piesat.cn:27022/ShuiLiDepartment/wrd.git(或https://github.com/leon1509/note.git)	// 把仓库关联到远程地址
   2.3 git add dictionary1/ dictionary1	// 再分别把多个本地项目上传本地仓库 变成红色感叹号图标
       git add dictionary2/ dictionary2
       .......
   2.4 git commit -m "初始化提交"	// 提交并填写注释
   2.5 git push origin master		// 把代码推送到远程仓库

   ======== 正常流程结束 ==========

   如果2.5报错，可能是远程仓库中存在部分文件是我们本地仓库不存在的 ，需要先pull下来。
   2.6 git pull --rebase origin master	// 把原先仓库中的文件pull下来
   2.7 git push -u origin master	// 再重新提交就可以了
````

### 4. IDEA将新建项目上传至GitLab
````
https://blog.csdn.net/weixin_30553065/article/details/99217824
````

### 5. 添加git用户邮箱和用户名
````
git config --global user.email "lutiansheng@piesat.com.cn"
git config --global user.name "lutiansheng"
````

### 6. 生成git密钥
````
ssh-keygen -t rsa -C "l.t...s....@p..s...com.cn"
````
