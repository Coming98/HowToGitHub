![image-20210427091136183](https://gitee.com/Butterflier/pictures/raw/master/images2/20210427091136.png)

# Quick Start

- Workspace：工作区 - 本地存放代码的目录
- Index / Stage：暂存区 - 
- Repository：仓库区（或本地仓库）
- Remote：远程仓库

~~~shell
git status # 查看本地库状态
git pull
git add .
git commit -m 'well'
git push origin
~~~

# Git

免费、开源的分布式版本控制系统

版本控制：记录文件内容变化，以便将来查阅特定版本修订情况的系统

集中式版本控制：一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。

缺陷：中央服务器单点故障问题

分布式版本控制：客户端提取的是整个代码仓库，每个客户端都是对远程库的完整备份，在远程库中进行版本控制

## 新建代码库

~~~shell
# 在当前目录新建一个Git代码库
$ git init

# 新建一个目录，将其初始化为Git代码库
$ git init [project-name]

# 下载一个项目和它的整个代码历史
$ git clone [url]
~~~

## 配置

Git的设置文件为`.gitconfig`，它可以在用户主目录下（全局配置），也可以在项目目录下（项目配置）。

~~~shell
# 显示当前的Git配置
$ git config --list

# 编辑Git配置文件
$ git config -e [--global]

# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
~~~

## 增加或删除文件

~~~shell
# 添加指定文件到暂存区
$ git add [file1] [file2] ...

# 添加指定目录到暂存区，包括子目录
$ git add [dir]

# 添加当前目录的所有文件到暂存区
$ git add .

# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p

# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ...

# 停止追踪指定文件，但该文件会保留在工作区
$ git rm --cached [file]

# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
~~~

## 提交代码

~~~shell
# 提交暂存区到仓库区
$ git commit -m [message]

# 提交暂存区的指定文件到仓库区
$ git commit [file1] [file2] ... -m [message]

# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a

# 提交时显示所有diff信息
$ git commit -v

# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...
~~~

## 分支处理

~~~shell
# 列出所有本地分支
$ git branch

# 列出所有远程分支
$ git branch -r

# 列出所有本地分支和远程分支
$ git branch -a

# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]

# 新建一个分支，并切换到该分支
$ git checkout -b [branch]

# 新建一个分支，指向指定commit
$ git branch [branch] [commit]

# 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 切换到上一个分支
$ git checkout -

# 建立追踪关系，在现有分支与指定的远程分支之间
$ git branch --set-upstream [branch] [remote-branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 选择一个commit，合并进当前分支
$ git cherry-pick [commit]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
~~~

## 标签

~~~shell
# 列出所有tag
$ git tag

# 新建一个tag在当前commit
$ git tag [tag]

# 新建一个tag在指定commit
$ git tag [tag] [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git push origin :refs/tags/[tagName]

# 查看tag信息
$ git show [tag]

# 提交指定tag
$ git push [remote] [tag]

# 提交所有tag
$ git push [remote] --tags

# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
~~~

## 查看信息

~~~shell
# 显示有变更的文件
$ git status

# 显示当前分支的版本历史
$ git log

# 显示commit历史，以及每次commit发生变更的文件
$ git log --stat

# 搜索提交历史，根据关键词
$ git log -S [keyword]

# 显示某个commit之后的所有变动，每个commit占据一行
$ git log [tag] HEAD --pretty=format:%s

# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
$ git log [tag] HEAD --grep feature

# 显示某个文件的版本历史，包括文件改名
$ git log --follow [file]
$ git whatchanged [file]

# 显示指定文件相关的每一次diff
$ git log -p [file]

# 显示过去5次提交
$ git log -5 --pretty --oneline

# 显示所有提交过的用户，按提交次数排序
$ git shortlog -sn

# 显示指定文件是什么人在什么时间修改过
$ git blame [file]

# 显示暂存区和工作区的差异
$ git diff

# 显示暂存区和上一个commit的差异
$ git diff --cached [file]

# 显示工作区与当前分支最新commit之间的差异
$ git diff HEAD

# 显示两次提交之间的差异
$ git diff [first-branch]...[second-branch]

# 显示今天你写了多少行代码
$ git diff --shortstat "@{0 day ago}"

# 显示某次提交的元数据和内容变化
$ git show [commit]

# 显示某次提交发生变化的文件
$ git show --name-only [commit]

# 显示某次提交时，某个文件的内容
$ git show [commit]:[filename]

# 显示当前分支的最近几次提交
$ git reflog
~~~

## 远程同步

~~~shell
# 下载远程仓库的所有变动
$ git fetch [remote]

# 显示所有远程仓库
$ git remote -v

# 显示某个远程仓库的信息
$ git remote show [remote]

# 增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]

# 取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force

# 推送所有分支到远程仓库
$ git push [remote] --all
~~~

## 撤销

~~~shell

# 恢复暂存区的指定文件到工作区
$ git checkout [file]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]

# 暂时将未提交的变化移除，稍后再移入
$ git stash
$ git stash pop
~~~

## Tips

~~~shell

# 生成一个可供发布的压缩包
$ git archive
~~~



# Git username

签名的作用是区分不同的作者身份，用户签名与GitHub等账号没有任何关系

**global**：设置全局用户签名

~~~shell
git config --global user.name "Coming" # set
git config --global user.name # check
git config --global user.email "email@example.com" # show
git config --global user.email # check 
~~~

**local**：about a single repository

~~~shell
git config user.name "Coming" # set
git config user.name # check
git config user.email "email@example.com" # show
git config user.email # check 
~~~

# Initial

获取目录的管理权：

~~~shell
git init
~~~

查看状态

~~~shell
git status
git reflog # 查看提交的版本
git log # 查看详细版本
~~~

# 增加或删除文件

~~~shell
$ git add [file1] [file2] ... # 添加指定文件到暂存区
$ git add [dir] # 添加指定目录到暂存区，包括子目录
$ git add . # 添加当前目录的所有文件到暂存区

# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p
############## 删除文件
$ git rm --cached [file] # 停止追踪指定文件，但该文件会保留在工作区
$ git rm [file1] [file2] ... # 删除工作区文件，并且将这次删除记录add到暂存区
$ git clean -f file # 删除未被追踪的文件
$ git clean -d dir
$ git rm -r --f file # 删除追踪 并 删除文件
$ git mv [file-original] [file-renamed] # 改名文件，并且将这个改名放入暂存区
~~~

# 忽略文件

与项目实际功能无关的一些文件

1. 家目录下创建忽略规则文件： `xxx.ignore` - `git.ignore`

2. 想忽略什么文件就写入其中即可，支持通配符 `*`

3. 在 `git.config` 中引入该文件 - 注意需要使用正斜线 `/`

   ~~~ssh
   [core]
   	excludesfile = 
   ~~~


# 提交代码

~~~shell
$ git commit -m [message] # 提交暂存区到仓库区
$ git commit [file1] [file2] ... -m [message] # 提交暂存区的指定文件到仓库区
$ git commit -a # 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -v # 提交时显示所有diff信息

# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...
~~~



# 回退版本

原理：每个版本有一个指针，指向某一版本；而当前用户有一个 head 指针，指向某一分支；通过移动指针，实现版本的迁移。

1. `git reflog` - 获取版本号
2. `git reset –hard 版本号`

# 分支管理

在版本控制过程中，同时推进多个任务，为每个任务，我们就可以创建每个任务的单独
分支。

![image-20210428094805835](https://gitee.com/Butterflier/pictures/raw/master/images2/20210428094813.png)

优势：并行推进任务，提高效率；分支开发失败不会对其它分支有任何影响

**相关命令**：branch

~~~shell
git branch -v # 查看分支信息
git branch branchName # 在当前版本创建新的分支
git checkout branchName # 切换到目标分支 
git merge branchName # 将 目标分支 合并到 当前分支
~~~

## 代码冲突问题

冲突产生的表现：后面状态为MERGING，表示正在合并中，没有合并成功

1. 两个分支在同一个文件  同一个位置  有两套完全不同的修改：人为指定新代码的内容

   > 打开文件后，git 已经帮你标明 不同分支 冲突所在
   >
   > ![image-20210428100919200](https://gitee.com/Butterflier/pictures/raw/master/images2/20210428100919.png)
   >
   > 选择需要留下的内容，保存文件
   >
   > `git add hello.txt` - 添加到暂存区
   >
   > `git commit -m “…”` - 提交到本地库 - 因为两个分支都修改了 hello.txt 因此 git 无法确定提交哪个hello.txt
   >
   > 注意合并结束后：只会修改当前分支的内容

# 团队协作

团队内协作：

![image-20210428105037154](https://gitee.com/Butterflier/pictures/raw/master/images2/20210428105048.png)

跨团队协作：

![image-20210428105106810](https://gitee.com/Butterflier/pictures/raw/master/images2/20210428105106.png)

# GitHub

全球最大同性交友网站，技术宅男天堂，新世界的大门

克隆目标仓库到本地：1. 拉取代码 2. 初始化本地库 3. 起别名：origin

~~~shell
git clone 仓库链接 
~~~

远程仓库别名：

~~~shell
git remote -v # 查看所有别名
git remote add 别名 库的链接 # 添加别名
~~~

推送别名：

~~~shell
git push 别名或连接 分支名
~~~

拉去内容到分支：同步

~~~shell
git pull 别名或连接 分支名
~~~

