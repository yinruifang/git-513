## 一.git 基础
	-- 网址：[](https://git-scm.com/book/zh/v2)
	--1.版本控制系统分类
		-- 本地版本控制
		-- 集中式版本控制
		-- 分布式版本控制 git
	--2.git 特点
		--直接记录快照，而非差异比较
		--近乎所有操作都是本地执行
		--Git 保证完整性
		--Git 一般只添加数据
	--3.三种状态
		已提交（committed） 表示数据已经安全地保存在本地数据库中
		已修改（modified）  表示修改了文件，但还没保存到数据库中
		已暂存（staged）    表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中
		
	--4.基本的 Git 工作流程如下：
		在工作区中修改文件。
		将你想要下次提交的更改选择性地暂存，这样只会将更改的部分添加到暂存区。
		提交更新，找到暂存区的文件，将快照永久性存储到 Git 目录。
			
## 二.git常用命令
	--1.基础配置和帮助
		git config --list    |  查看配置项
		git config --global user.name "英文名或中文名的拼音"   | 设置名字  
		git config --global user.email "邮箱"   | 设置邮箱地址
		git help | 帮助文档
	--2.git的基础三步命令
		定位到git的文件夹  打开 E:/gitcode 文件夹，点右键  在菜单里选择 Git Bash Here
		
		git init  | 初始化
		
		添加新文件到git仓库
		
		git add 文件名  | 将要跟踪的某个文件放入暂存区
		git commit -m "说明" | 将文件提交到git仓库
		git status | 查看状态
		
		git add *    | 将所有的要跟踪的文件全部放入暂存区域
		git add .    |  将所有新增或修改状态的文件加入到暂存区域
		
		
	--3.git 新增 修改 删除后的状态
		--新增
		在文件夹中添加 a.txt  b.txt c.txt
		git status   | 查看状态
```
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   a.txt
		```
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        new file:   b.txt
        new file:   c.txt
		```
		git add * | 加入暂存区
		git commit -m "新增了a文件 b文件 c文件"  | 提交到 git仓库
		
		-- 修改
		打开文件 a.txt  输入内容  保存
		git status 
```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
        modified:   a.txt
no changes added to commit (use "git add" and/or "git commit -a")
		```
		git add * 
		git commit -m "修改了文件"
		
		-- 删除
		删除 c.txt  
		git status
```
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
        deleted:    c.txt
no changes added to commit (use "git add" and/or "git commit -a")
		```
		git rm b.txt c.txt 
		git commit -m "删除了b文件 c文件"
		
	--4.忽略文件的做法
		a.在hbuilder 中创建.gitignore的文件
		b.将 tt.txt 和 .gitignore 写到该文件中
```
tt.txt
.gitignore
		```
		c.执行 git status 操作，发现 tt.txt 不被跟踪了
		
	--5.修改文件时查看文件的具体差异  git diff 
		a.修改了 a.txt 文件
		b. 执行 git diff 命令，会显示出修改了具体哪些内容
```
diff --git a/a.txt b/a.txt
index 40ae540..aeb9123 100644
--- a/a.txt
+++ b/a.txt
@@ -1,3 +1,4 @@
 git<B5><C4><C3><FC><C1><EE>
 <C8><F6><B4><F2><B7><A2>˹<B5>ٷ<D2>
 <C8><F8><B4><EF><CA>Ƿ<F1>
+console.log("hello");
		```
		c. git add *
		d. git status 
		e. git commit -m "修改了文件"
		
	--6.删除文件  ，将git仓库中的文件也进行了删除
		git rm 'aa.html'
		git status
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        deleted:    aa.html
		```
		git commit -m "删除文件"
		
	--7.移动文件
		git mv aa.css src/aa.css
	
	--8.查看日志
		git log 
		注意：如果记录比较多，一屏显示不全，到end，光标没有跳出，我们可以按 ctrl+c  ,还可以输入 :q
		--查询近两次的历史记录
		git log -p -2
		--简单的统计操作
		git log -p -2 --stat
		--指定格式显示
		git log --pretty=oneline
		--按照需要的配置显示内容
		git log --pretty=format:"%h - %an, %ar : %s"
		--按照区间
		git log --pretty="%h - %s" --since="2020-11-30" --before="2020-12-01"
	--9.撤销提交，修改提交的提示语  
		git commit --amend 
		注意：按i键进入修改操作，修改完后，按esc键，再按:wq进行保存，跳出编辑状态
	--10.取消暂存的文件
		a.新增了ce.html  修改了 yyy.js
		b.git status  查看状态
```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
        modified:   yyy.js
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ce.html
no changes added to commit (use "git add" and/or "git commit -a")
```
		c. git add *
```
The following paths are ignored by one of your .gitignore files:
tt.txt
Use -f if you really want to add them.
warning: LF will be replaced by CRLF in ce.html.
The file will have its original line endings in your working directory
		```
		d. git status
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        new file:   ce.html
        modified:   yyy.js
		```
		e.问题：ce.html不想提交
		git commit -m 'asdfaf'  两个文件一起提交仓库
		
		f.取消暂存
		git reset HEAD ce.html   
		
		git status
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        modified:   yyy.js
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        ce.html
		```
	执行完取消暂存后，ce.html就不会被提交，只有 yyy.js被提交
		
	--11.将单个文件的修改还原到上一个版本
	git checkout ce.html
	注意，该用法只适用于文件修改后并没有加入暂存区的  ，没有执行过  git add *	
	
	--12.	还原整个项目的历史版本信息    2c5f117121f1189bcd44df96b840084af7a417de
	git reset --hard  版本号
	注意：尽量不要执行这个操作，如果执行，请记录好最新的版本号
	
## 三.	远程仓库 
	--1.创建一个文件夹  E:/yuan 
	--2.在文件夹中右键菜单，打开 git bash
	--3.git init 初始化
	--4.git clone  https://github.com/yinruifang/houniao.git  | 下载远程的代码包到本地  *****

## 四. 将本地仓库和远程仓库关联
	--在E:创建文件夹 gityuancheng
	--进入文件夹，打开 git bash
	-- git init
	--在gityuancheng 创建新文件 README.md
	--git add *
	--git commit -m '第一次提交'
	
	--打开gihub网站
	--登录
	--网站的右上角点击 加号，选择 New repository,进去创建新项目
	--需要添加项目名称和项目描述，点确定按钮
	--git remote add origin https://github.com/yinruifang/yuancheng.git  | 将本地代码库和远程代码库关联
	--git remote -v | 查看远程仓库
```
origin  https://github.com/yinruifang/yuancheng.git (fetch)
origin  https://github.com/yinruifang/yuancheng.git (push)
	```
	--git push -u origin master  将本地代码推到远程仓库
	
	--如果本地仓库有修改或者新增，需要执行以下几步：
	1.git add *
	2.git commit -m "备注内容"
	3.git push -u origin master
	
	--如果github上有变化
	git pull origin master  进行拉取操作
	
	git fetch origin master 拉取
	
	区别：git pull 相当于 git fetch + get merge（合并）
	
## 五.对 代码打tag标签， 标签是版本号，代码打包  指的就是 git上将稳定的代码包打标签
	1. git tag v0.0.1(版本号)   打tag包 ，目的是将稳定版本可以发布服务器
	2. git tag | 查看所有tag
	3. git tag -a v0.1.1 -m "包稳定，明天发版"   | 给 tag包写注释
	4. git show v0.1.1 显示某个版本的一些具体信息

## 六.分支
	-- 1.创建分支
	git branch 分支名
	--2.切换分支
	git checkout 分支名
	--3.合并分支
	git merge 分支名
	--4.合并分支时出现了冲突怎样解决
	冲突的原因是：两个分支，有一样的文件名，内容不一样，合并时就会有冲突
```
CONFLICT (add/add): Merge conflict in b.txt
Auto-merging b.txt
Automatic merge failed; fix conflicts and then commit the result.
	```
	解决方法：将冲突文件打开，将冲突的内容手动修改
	执行 ：git add *
	git commit -m "解决冲突"

## 七.git 小乌龟的使用
	--1.安装
	--2.在E:创建文件夹tocode
	--3.在tocode中点击右键  git在这里创建版本库
	--4.拷贝5个文件进来
	--5.点击右键，选择 添加 操作  | 添加到暂存区
	--6.点击右键 ，选择 提交操作  | 提交到本地代码库
	--7.在 github上添加新的项目
	--8.点击右键 ，选择推送操作   |  目标  -  远端   -  管理 
	将 远端  和 url填写上
	需要填写用户名和密码
	

## 常用命令 [](https://www.cnblogs.com/miracle77hp/articles/11163532.html)		
git init   *****  项目初始时执行一次初始化操作就可以了
git config  ***** 设置用户名和邮箱
git clone   ***** 将远程仓库的代码复制到本地
git remote add origin  *** 关联远程仓库
git push   *****  将本地代码推到远程仓库
git pull   **** 拉取代码
git fetch  ***  拉取代码
git tag ****    给代码打包
git branch ***** 创建分支
git checkout ***** 切换分支
git merge *****   合并分支

可以执行多次，只要有新增、修改、删除 都需要执行以下三步走
git add    *****  添加到暂存区
git commit *****  提交代码到git仓库
git status *****  查看状态

git rm   ***      删除 git仓库中的文件
git log  ***      查看日志文件
git help *        帮助文档
git mv   *        移动文件



## 作业
1.请在 github上创建一个新的代码库，上传js或者es6或者html5的代码，将 git地址提交到微信群
2.git 常用命令 单词记忆
3.ceshi

