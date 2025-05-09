#### 1.安装
#### 2.本地仓库
它的仓库结构和linux系统是相似的，但其根目录是Git的安装路径

而它的文件系统结构，也认定**一切皆文件**

linux中的/home/user,一般在根目录下

而Git的文件系统结构虽然也是从根结点出发，但是windows的C盘、D盘都是默认挂载在根节点下。
比如/c是c盘，/d是D盘
![[Pasted image 20250420124830.png]]
所以Git的文件系统有一个回路，连接着Git的安装目录和所在的盘

回到默认工作路径
```
cd ~
```

而一般，Git的Bash命令行会在/c/user下启动，同时在以后拉取项目时，不指定路径则默认放在此处。
![[Pasted image 20250420123232.png]]

因此，创建一个目录，存放拉取的项目
![[Pasted image 20250420124653.png]]
##### 1.设置用户信息

```
#设置用户信息和邮箱
git config --global user.name wowuluya
git config --global user.email chuanxiayang@outlook.com
```
用户配置文件会在设置后，自动创建存储在/C/Users/admin下，
![[Pasted image 20250420125424.png]]

##### 2.创建本地仓库
```
#在指定位置创建本地仓库（不指定路径时，默认在当前工作目录下创建）
git init /d/Soft/Git/Git-repository

```
##### 3.查看仓库分支
需要在含有.git的仓库路径下才行
```
#查看所有分支
git branch -a

#查看远程分支
git branch -r
```
##### 4.查看仓库状态
```
git status
```
![[Pasted image 20250420143441.png]]
```
#图片git命令下为：
在master分支下

初始化仓库的首次提交

没有东西提交
```
![[Pasted image 20250420143617.png]]
```
在master分支下

没有提交的记录

未被跟踪的文件，即不在git管理中的文件，不在版本控制范围中的文件
```
![[Pasted image 20250420144010.png]]
```
在master分支下
没有提交记录
提交前的改变（即暂存区）
未暂存的提交更改（工作区变动，但暂存区未变）
```
##### 5.添加到暂存区
```
#将部分文件添加到暂存区
git add 文件/文件夹名 [文件]
#将所有文件添加到暂存区
git add .
#将特定类型文件添加到暂存区
git add *.txt

#将以.xml为后缀的文件添加到暂存区
git add *.xml
```
![[Pasted image 20250420153707.png]]
##### 6.提交本地仓库
```
#提交指定文件
git commit -m "提交说明信息，便于回溯" 暂存区文件名

#提交全部文件（包括未更新的跟踪文件
git commit -a -m "提交信息说明"

#实例
git commit -m "首测提交" 
```
![[Pasted image 20250420154411.png]]
\* master 表明当前处于master分支下，并且之后的操作都基于此分支。

##### 7.创建和切换分支
```
#创建分支
git branch 分支名

#切换分支
git checkout 分支名

#创建并切换分支
git checkout -b 分支名

#举例
git branch 1.0
```
![[Pasted image 20250421144236.png]]
\* 1.0 则代表当前处于1.0分支下

**创建分支是基于当前所在的分支（\* 标识的分支）复制的**

```
#查看两个分支差异
git diff 分支1..分支2

示例
git diff master..1.0
```
![[Pasted image 20250421145931.png]]
从$ git行往下：
比较a和b的差异，a即master，b即1.0  ，比较各自的file01的差异
index  表示这两个文件的哈希值的差异    003064c是a的哈希值，e69de29是b的哈希值    100644表示文件的权限
\--- 表示原始文件，a也是原始文件的表示
\+++ 表示目标文件，b是目标文件的表示
@@为差异块标识符   -1表示原始文件第1行有变化  +0,0表示目标文件第0行开始比较，停留在第0行，即该文件为空
-this... 表示a原始文件的标注


##### 8.删除分支
```
#不能在目标分支下删除该分支
#需要先切换别的分支
git checkout master

#删除分支
git branch -d 分支名

#举例
git checkout master
git branch -d 1.0
```
![[Pasted image 20250421151619.png]]
##### 9.合并分支
```
#切换要合并到的分支（目标分支）
git checkout master

#合并分支(将指定分支合并到当前分支)
git merge 1.1

#举例:将1.1分支合并到master分支
git checkout master
git merge 1.1
```
![[Pasted image 20250421152928.png]]


### 3.关联远程仓库

在github上新创建仓库
![[Pasted image 20250509152640.png]]

关联仓库
```
#git remote add origin <httpsURL>
git remote add origin https://github.com/wowuluya/A-new-and-first-repository.git

```

上传
```
#git push origin <分支名>
git push origin master
```
![[Pasted image 20250509153542.png]]
然后通过链接验证后，就能将master分支内容上传
