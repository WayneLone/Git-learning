# 目录
1. Git简介
    - 1.1 Git的诞生
    - 1.2 集中式vs分布式
2. 安装Git
3. 创建版本库
4. 时光机穿梭
    - 4.1 版本回退
    - 4.2 工作区和暂存区
    - 4.3 管理修改
    - 4.4 撤销修改
    - 4.5 删除文件
5. 远程仓库
    - 5.1 添加远程库
    - 5.2 从远程库克隆
6. 分支管理
    - 6.1 创建与合并分支
    - 6.2 解决冲突
    - 6.3 分支管理策略
    - 6.4 Bug分支
    - 6.5 Feature分支
    - 6.6 多人协作
7. 标签管理
    - 7.1 创建标签
    - 7.2 操作标签
8. 使用GitHub
9. 使用码云
10. 自定义Git
    - 10.1 忽略特殊文件
    - 10.2 配置别名
    - 10.3 搭建Git服务器
11. 期末总结

------------------------------------------------

## 1. Git简介
Git是什么？  
Git是目前世界上最先进的分布式版本控制系统（没有之一）。  
Git有什么特点？简单来说就是：高端大气上档次！
### 1.1 Git的诞生
两周时间完成开发,一个月正式使用,Linus 牛!
### 1.2 集中式vs分布式
SVN,CVS等是集中式的版本库控制系统,版本库存在中央服务器上,需要联网才能工作.  
Git是分布式的版本库控制系统,每个人的电脑上都是完整的版本库.
## 2.安装Git
> 实话实说，Windows是最烂的开发平台，如果不是开发Windows游戏或者在IE里调试页面，一般不推荐用Windows。

1. 下载地址:[https://git-for-windows.github.io/](https://git-for-windows.github.io/)
2. 打开Git Bash
3. 设置用户名和email  
    `$ git config --global user.name "Your Name"`  
    `$ git config --global user.email "email@example.com"`
4. `--global` 表示这台机器上所有的Git仓库都会使用这个配置
## 3.创建版本库
> 版本库:repository  
> 你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。  

> 所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。
### Linux操作命令
- cd 改变目录(change directory)
    + cd 主目录
    + cd .. 上一级目录
- mkdir 创建文件夹
- pwd 显示当前目录
- ls 显示当前目录文件列表
    + ls -a 查看全部文件,包括隐藏文件
- cat 显示文件内容
- rm 删除文件
### 操作步骤
1. 创建空目录
2. 进入文件夹
3. 初始化文件目录,变成Git可管理的仓库`git init`
4. 将需要管理的文件放在Git仓库
5. 在Git中使用命令添加`git add <file>`
    - 可反复多次使用,添加多个文件
6. 提交修改`git commit -m "提交说明"`
## 4.时光机穿梭
- git status
    + 掌握当前仓库的状态
- git diff
    + 查看修改的内容
### 4.1 版本回退
- git log
    + 提交历史记录
    + `git log --pretty=oneline`简略信息
- HEAD
    + 当前版本,也就是最新的提交
    + HEAD^ : 上个版本,HEAD^ : 上上个版本,HEAD~100,往上100个版本
- git reset --hard commit_id
    + commit_id不必写全,写前几位能定位到就可以
- git reflog
    + 查看提交历史,可以查到未来的commit_id,回到未来
### 4.2 工作区和暂存区
#### 工作区(Working Directory)
就是你在电脑里能看到的目录
#### 版本库(Repository)
> 工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。  
> Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

> 前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：  
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；   
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。  
因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。

![](img/gitadd.jpg)
![](img/gitcommit.jpg)

> 所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。
> 一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的
```
    $ git status
    On branch master
    nothing to commit, working tree clean
```
### 4.3 管理修改
> 为什么Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。  
> 每次修改，如果不add到暂存区，那就不会加入到commit中。
### 4.4 撤销修改
- `git checkout -- <file>`
> 命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：  
>> 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；  
>> 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。 
> 
> 总之，就是让这个文件回到最近一次git commit或git add时的状态。
- `git reset HEAD <file>`
    + 可以把暂存区的修改撤销掉（unstage）,重新放回工作区
#### 小结
**场景1**：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

**场景2**：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD` file，就回到了场景1，第二步按场景1操作。
> 也可以使用`git reset --hard HEAD`,直接将提交的最后一个版本恢复,此时暂存区也会清空
 
**场景3**：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

### 4.5 删除文件
#### 从版本库中删除文件
- git rm
    + 命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
- git commit
## 5.远程仓库
- 用户主目录
    + C:\Users\lianz
- 创建SSH key
    + `$ ssh-keygen -t rsa -C "youremail@example.com"`
    + 创建完成后用户主目录下会有id_rsa和id_rsa.pub两个文件
    + 因为有用GitHub客户端,所以还有github_rsa和github_rsa.pub文件
- 添加至GitHub设置
### 5.1 添加远程库
- 在GitHub上创建同名仓库
- 根据提示把本地库的所有内容推送到服务器上
    + `$ git remote add origin git@github.com:michaelliao/learngit.git`
    + `$ git push -u origin master`

> 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

- `$ git push origin master`
    + 之后就可以使用此命令进行推送
### 5.2 从远程库克隆
## 6.分支管理
### 6.1 创建与合并分支
### 6.2 解决冲突
### 6.3 分支管理策略
### 6.4 Bug分支
### 6.5 Feature分支
### 6.6 多人协作
## 7. 标签管理
### 7.1 创建标签
### 7.2 操作标签
## 8. 使用GitHub
## 9. 使用码云
## 10. 自定义Git
### 10.1 忽略特殊文件
### 10.2 配置别名
### 10.3 搭建Git服务器
## 11. 期末总结