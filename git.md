### 1. 删除项目与git的关联关系（Idea 2020.3版本）
````
  1.1 Idea中，项目右键-->Git-->Manage Remotes，减号删除项目与git的关联关系。
  1.2 进入项目目录，删除.git目录
  1.3 Idea中，File-->Settings-->Version Control，减号删除右边的关联关系。
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
