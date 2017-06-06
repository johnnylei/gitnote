## git 笔记
> git 工作流程

- git svn 区别
    - GIT是分布式的，SVN不是：这是GIT和其它非分布式的版本控制系统，例如SVN，CVS等，最核心的区别（任意的一个git，可以被clone,或是update去远端）。
    - GIT把内容按元数据方式存储，而SVN是按文件：所有的资源控制系统都是把文件的元信息隐藏在一个类似.svn,.cvs等的文件夹里。
    - GIT分支和SVN的分支不同：分支在SVN中一点不特别，就是版本库中的另外的一个目录。
    - GIT没有一个全局的版本号，而SVN有：目前为止这是跟SVN相比GIT缺少的最大的一个特征。
    - GIT的内容完整性要优于SVN：GIT的内容存储使用的是SHA-1哈希算法。这能确保代码内容的完整性，确保在遇到磁盘故障和网络问题时降低对版本库的破坏。
    
- 工作流程
![image](/src/img/work_flow.png)
- 基本概念
    - 
    - 工作区：目录
    - 暂存区：
        - 执行add命令之后，暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中（.git/index）。
        - commit,暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。
        - git reset HEAD, 暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。
        - git rm --cached <file>,会直接从暂存区删除文件，工作区则不做出改变。
        - git checkout ./git checkout -- <file> 会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区的改动。
        - git checkout HEAD ./git checkout HEAD <file> 会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。
- 基本命令
    - git init 生成repository
    - 将别人的ssh pub key 放入到 ~/.ssh/authorized_keys 中
    - 通过git clone（-b 指定branch）
    - 如果不指定-b则理论上来讲是默认master分支
    - git add 将想要快照的内容写入缓存，
    - git commit 记录缓存区的快照
    - git push/git push提交和拉取
    - git config 设置配置文件
    - git branch可以查看当前project的branch
    - git branch -a 可以查看所有的Branch
    - git checkout (brank) 切换branch
    - git branch (branch) 创建branch
    - git meger (branch) 可以将别的branch meger过来
    - git checkout -b (localbarnchname)  (remotebranchname) 可以从远端checkout 你想要的分支（因为clone的时候，只能clone一个分支）
    - git diff HEAD 查看所有的diff
    - git diff 尚未缓存的改动
    - git diff --cached 查看已缓存的改动
    - git log oneline 简单Log
    - git log --graph 类似于画图
    - git status/git status -s 以查看在你上次提交之后是否有修改。
    - git tag -a v1.0 定义版本号
    - git log --online --decorate -graph/git tag -a v0.9 85fc7e7 可以查看版本号
- 配置github环境
    - ssh-keygen -t rsa -C "leiyuqing_jing@163.com", 这个邮箱地址应该为github绑定的邮箱地址
    - 回到github上，进入 Account Settings（账户配置），左边选择SSH Keys，Add SSH Key,title随便填，粘贴在你电脑上生成的key。
    - ssh -T git@github.com 验证是否联系github成功
    - 在github上面创建repostory, 根据github上提供的地址，git remote add origin git@github.com:tianqixin/w3cschool.cc.git
    - 配置.git 里面的config 文件，来指定不同路径
```
[remote "72server"]
	
url = www@121.40.213.72:/tmp/project/.git
	
fetch = +refs/heads/*:refs/remotes/b2/*

[branch "b2"]
	
remote = b2
	
merge = refs/heads/b2

[remote "gitserver"]
	
url = https://github.com/johnnylei/first.git
	
fetch = +refs/heads/*:refs/remotes/b2/*

[remote "all"]  
    url = https://github.com/johnnylei/first.git
  
    fetch = +refs/heads/*:refs/remotes/b2/*
    url = www@121.40.213.72:/tmp/project/.git
    fetch = +refs/heads/*:refs/remotes/b2/*
```
- 高阶命令
    - git remote/git remote -v查看远端信息
    - git fetch 从远程仓库下载新分支与数据,该命令执行完后需要执行git merge 远程分支到你所在的分支
<<<<<<< HEAD
    - git push [alias] [branch]/ git pull [alias] [branch] 指定远端和分支
- 命令手册

```
git init                                                  # 初始化本地git仓库（创建新仓库）
git config --global user.name "xxx"                       # 配置用户名
git config --global user.email "xxx@xxx.com"              # 配置邮件
git config --global color.ui true                         # git status等命令自动着色
git config --global color.status auto
git config --global color.diff auto
git config --global color.branch auto
git config --global color.interactive auto
git clone git+ssh://git@192.168.53.168/VT.git             # clone远程仓库
git status                                                # 查看当前版本状态（是否修改）
git add xyz                                               # 添加xyz文件至index
git add .                                                 # 增加当前子目录下所有更改过的文件至index
git commit -m 'xxx'                                       # 提交
git commit --amend -m 'xxx'                               # 合并上一次提交（用于反复修改）
git commit -am 'xxx'                                      # 将add和commit合为一步
git rm xxx                                                # 删除index中的文件
git rm -r *                                               # 递归删除
git log                                                   # 显示提交日志
git log -1                                                # 显示1行日志 -n为n行
git log -5
git log --stat                                            # 显示提交日志及相关变动文件
git log -p -m
git show dfb02e6e4f2f7b573337763e5c0013802e392818         # 显示某个提交的详细内容
git show dfb02                                            # 可只用commitid的前几位
git show HEAD                                             # 显示HEAD提交日志
git show HEAD^                                            # 显示HEAD的父（上一个版本）的提交日志 ^^为上两个版本 ^5为上5个版本
git tag                                                   # 显示已存在的tag
git tag -a v2.0 -m 'xxx'                                  # 增加v2.0的tag
git show v2.0                                             # 显示v2.0的日志及详细内容
git log v2.0                                              # 显示v2.0的日志
git diff                                                  # 显示所有未添加至index的变更
git diff --cached                                         # 显示所有已添加index但还未commit的变更
git diff HEAD^                                            # 比较与上一个版本的差异
git diff HEAD -- ./lib                                    # 比较与HEAD版本lib目录的差异
git diff origin/master..master                            # 比较远程分支master上有本地分支master上没有的
git diff origin/master..master --stat                     # 只显示差异的文件，不显示具体内容
git remote add origin git+ssh://git@192.168.53.168/VT.git # 增加远程定义（用于push/pull/fetch）
git branch                                                # 显示本地分支
git branch --contains 50089                               # 显示包含提交50089的分支
git branch -a                                             # 显示所有分支
git branch -r                                             # 显示所有原创分支
git branch --merged                                       # 显示所有已合并到当前分支的分支
git branch --no-merged                                    # 显示所有未合并到当前分支的分支
git branch -m master master_copy                          # 本地分支改名
git checkout -b master_copy                               # 从当前分支创建新分支master_copy并检出
git checkout -b master master_copy                        # 上面的完整版
git checkout features/performance                         # 检出已存在的features/performance分支
git checkout --track hotfixes/BJVEP933                    # 检出远程分支hotfixes/BJVEP933并创建本地跟踪分支
git checkout v2.0                                         # 检出版本v2.0
git checkout -b devel origin/develop                      # 从远程分支develop创建新本地分支devel并检出
git checkout -- README                                    # 检出head版本的README文件（可用于修改错误回退）
git merge origin/master                                   # 合并远程master分支至当前分支
git cherry-pick ff44785404a8e                             # 合并提交ff44785404a8e的修改
git push origin master                                    # 将当前分支push到远程master分支
git push origin :hotfixes/BJVEP933                        # 删除远程仓库的hotfixes/BJVEP933分支
git push --tags                                           # 把所有tag推送到远程仓库
git fetch                                                 # 获取所有远程分支（不更新本地分支，另需merge）
git fetch --prune                                         # 获取所有原创分支并清除服务器上已删掉的分支
git pull origin master                                    # 获取远程分支master并merge到当前分支
git mv README README2                                     # 重命名文件README为README2
git reset --hard HEAD                                     # 将当前版本重置为HEAD（通常用于merge失败回退）
git rebase
git branch -d hotfixes/BJVEP933                           # 删除分支hotfixes/BJVEP933（本分支修改已合并到其他分支）
git branch -D hotfixes/BJVEP933                           # 强制删除分支hotfixes/BJVEP933
git ls-files                                              # 列出git index包含的文件
git show-branch                                           # 图示当前分支历史
git show-branch --all                                     # 图示所有分支历史
git whatchanged                                           # 显示提交历史对应的文件修改
git revert dfb02e6e4f2f7b573337763e5c0013802e392818       # 撤销提交dfb02e6e4f2f7b573337763e5c0013802e392818
git ls-tree HEAD                                          # 内部命令：显示某个git对象
git rev-parse v2.0                                        # 内部命令：显示某个ref对于的SHA1 HASH
git reflog                                                # 显示所有提交，包括孤立节点
git show HEAD@{5}
git show master@{yesterday}                               # 显示master分支昨天的状态
git log --pretty=format:'%h %s' --graph                   # 图示提交日志
git show HEAD~3
git show -s --pretty=raw 2be7fcb476
git stash                                                 # 暂存当前修改，将所有至为HEAD状态
git stash list                                            # 查看所有暂存
git stash show -p stash@{0}                               # 参考第一次暂存
git stash apply stash@{0}                                 # 应用第一次暂存
git grep "delete from"                                    # 文件中搜索文本“delete from”
git grep -e '#define' --and -e SORT_DIRENT
git gc
git fsck
```

>解决conflict的流程
- git add ., git commit -m 'message', 这样之后，工作去的改变就会存入到缓存中去
- git pull, 如果服务器这边有变动，就会生成需要你去meger的消息提醒，解决了conflict(git show <commit>,可以查看相关信息)
- 之后，就可以Push上远端了

>解决gitignore失效
```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```
