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
- `git clone`
    + `git clone git@github.com:KeKe-Li/vue.git`
    + 克隆一个别人的项目
    + 地址可以在项目页面找到

> GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。

> 使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。

## 6.分支管理
### 6.1 创建与合并分支
- `git branch`
    + 查看分支
- `git branch <name>`
    + 创建分支
- `git checkout <name>`
    + 切换分支
- `git checkout -b <name>`
    + 创建 + 切换分支
- `git merge <name>`
    + 合并某分支到当前分支
- `git branch -d <name>`
    + 删除分支

> 每次提交Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，**HEAD指向的就是当前分支**。

> 因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。

### 6.2 解决冲突
1. 当合并分支遇到冲突时,需手动修改文件并完成合并
2. 修改后使用`git add` + `git commit`命令重新提交
3. 提交完成后删除被合并的分支

- `git log --graph`
    - 命令可以看到分支合并图
    - `git log --graph --pretty=oneline --abbrev-commit`
    - 加参数可以简化显示
### 6.3 分支管理策略
#### fast forward
> 通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。

> 如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

- `--no-ff`
    + `git merge --no-ff -m "merge with no-ff" dev`
    + 因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去

#### 分支策略
> 在实际开发中，我们应该按照几个基本原则进行分支管理：

> 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

> 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

> 你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

所以，团队合作的分支看起来就像这样：  
![](img/branch.png)
### 6.4 Bug分支
- `git stash`
    + 可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作
- `git stash list`
    + 查看stash列表
- `git stash pop`
    + 恢复现场的同时删除stash内容
- `git stash apply`
    + 只恢复现场,不删除stash内容
- `gir stash drop`
    + 删除stash内容
- 多次stash恢复
    + 先用`git stash list`查看,再恢复指定stash
    + `git stash apply stash@{0}`

> 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

> 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。


### 6.5 Feature分支
- `git branch -D <name>`
    - 强行删除一个没有经过合并的分支

> 开发一个新feature，最好新建一个分支；

> 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

### 6.6 多人协作
- `git remote`
    + 查看远程库的信息
    + `git remote -v`
    + 远程库的详细信息,包括抓取和推送地址,如果没有推送权限,就看不到push地址
#### 推送抓取分支
> master分支是主分支，因此要时刻与远程同步；

> dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

> bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

> feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

#### 多人协作模式
1. 首先，可以试图用`git push origin branch-name`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！
> 如果git pull提示“`no tracking information`”，则说明本地分支和远程分支的链接关系没有创建，用命令  
> `git branch --set-upstream branch-name origin/branch-name`。

#### 小结
- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

## 7. 标签管理
> 发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。  

> tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。
### 7.1 创建标签
- 命令`git tag <name>`用于新建一个标签，默认为`HEAD`，也可以指定一个`commit id`；
- `git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- `git tag -s <tagname> -m "blablabla..."`可以用PGP签名标签；
- 命令`git tag`可以查看所有标签。
- `git show <tagname>`可以查看说明文字

### 7.2 操作标签
- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。
> 已经推送的标签要先从本地删除,再从远程删除
## 8. 使用GitHub
> 一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地址git@github.com:twbs/bootstrap.git克隆，因为没有权限，你将不能推送修改。
## 9. 使用码云
## 10. 自定义Git
- `git config --global color.ui true`
    + 让Git显示颜色,会使命令输出看起来更醒目
### 10.1 忽略特殊文件
#### 忽略文件的原则
1. 忽略操作系统自动生成的文件，比如缩略图等；
2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。
#### 小结
- `git add -f <file>`
    + 强制将已忽略的文件添加至Git
- `git check-ignore -v App.class`
    + 检查是哪一条规则忽略了该文件
- 忽略某些文件时,需要编写`.gitignore`
- `.gitignore`文件本身要放到版本库里,并且可以对`.gitignore`做版本管理
### 10.2 配置别名
- `git config --global alias.st status`
- 每个仓库的配置文件放在.git/config
- 全局的配置文件放在用户主目录下.gitconfig
```
[alias]
    st = status
    co = checkout
    ci = commit
    br = branch
    unatage = reset HEAD
    last = log -1
    lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
```
### 10.3 搭建Git服务器
## 11. 期末总结
完结撒花~~~