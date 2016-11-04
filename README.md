##### git 笔记
> git 工作流程


- 工作流程
![image](http://www.phpxs.com/uploads/201509/22/14428898011.png)
- 基本概念
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
    - 
