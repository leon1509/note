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

### 3. 使用git命令 提交多个项目到同一个仓库中
````
https://www.pianshen.com/article/97731377065/
````

### 4. IDEA将新建项目上传至GitLab
````
https://blog.csdn.net/weixin_30553065/article/details/99217824
````
