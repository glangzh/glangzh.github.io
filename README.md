# glangzh.github.io

* master: 主分支，主要用来版本【发布】。
* develop：日常开发分支，该分支正常保存了【开发的最新代码】。
* feature：具体的功能开发分支，只与 develop 分支交互。由具体的开发者在本地创建
* release：release 分支可以认为是 master 分支的未测试版。如某一功能全部开发完成，那么就将 develop 分支合并到 release 分支，测试没有问题并且到了发布日期就合并到 master 分支，打tag，进行发布。
* hotfix：线上 bug 修复分支。由master分支切出，修复后合并到master，develop分支，添加对应tag。

### master:
    $ git checkout master
    $ git pull

### develop: 日常开发分支,各个开发者fork此分支到本地
    $ git checkout develop
    $ git checkout -b develop master （创建并切换到develop分支）
    或
    $ git checkout -b develop origin/develop (checkout 远程develop到本地)
### 同步远程develop
    $ git checkout develop
    $ git pull origin develop
    或
    $ git fetch origin develop
    $ git merge origin/develop
    或
    $ git fetch origin develop
    $ git rebase origin/develop
    $ git push / git push -u origin develop

### feature: 从develop分支建一个feature分支,并切换到feature分支,进行新功能开发
    $ git checkout -b feature-xxx develop
    
    开发完成合并feature到develop分支
    $ git checkout develop
    $ git merge -no-ff feature-xxx
    $ git push -u origin develop

### release: 发布版本前的待测试版
    $ git checkout -b release-x.x.x develop
    
    更新版本信息，修复测试中的bug
    $ git commit -a -m 'update version number to XXX'
### release 分支合并到 master 分支, 标记 tag (发布版本信息)
    $ git checkout master
    $ git merge --no-ff release-x.x.x
    $ git tag -a x.x.x / git tag -a x.x.x -m '***'
    $ git push -u origin master
    $ git push origin x.x.x / git push origin --tags (推送本地标签到远程仓库)
    
    # release 分支合并到 develop 分支
    $ git checkout develop
    $ git merge --no-ff release-x.x.x
    $ git push -u origin develop
### 删除 release 分支
    $ git branch -d release-x.x.x

### hotfix: 从master分支切出，修复完成后合并到master，develop分支
    $ git checkout -b hotfix-x.x.x master
    $ git commit -m 'fixed ***'
    $ git checkout master / git merge --no-ff hotfix-x.x.x
    $ git checkout develop / git merge --no-ff hotfix-x.x.x
    $ git branch -d hotfix-x.x.x
    $ git push -u origin master
    $ git push -u origin develop
