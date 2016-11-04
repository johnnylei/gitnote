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
    - 