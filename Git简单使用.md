Git简单使用
-----------------------

> 参考文章[《在GitHub上管理项目》][2]

###git初始化
> 在使用git进行代码管理之前，首先要对git进行初始化

设置名字和email,这些是你在提交commit时的签名，每次提交记录里都会包含这些信息

    $ git config --global user.name "TongxinV"
    $ git config --global user.email "liyanbin0027@163.com"
    
禁用自动转换，避免出现`warning: LF will be replaced by CRLF`：

    $ git config --global core.autocrlf false  

执行了上面的命令后,会在家目录(/home/shiyanlou)下建立一个叫.gitconfig 的文件（该文件为隐藏文件，需要使用ls -al查看到）. 内容一般像下面这样，可以使用vim或cat查看文件内容:

    $ cat ~/.gitconfig
    [filter "lfs"]
            clean = git-lfs clean -- %f
            smudge = git-lfs smudge -- %f
            required = true
    [user]
            name = TongxinV
    [user]
            email = liyanbin0027@163.com
    [gui]
            recentrepo = F:/git_project
    [core]
            autocrlf = false
            
上面的配置文件就是Git全局配置的文件，一般配置方法是git config --global <配置名称> <配置的值>

###本地新建repository
> 可以本地建立文件夹再右键，也可以在git命令行下mkdir

本地仓库初始化：

    $ git init

###与远程仓库建立链接：

> 具体参考这篇文章[简单使用Git和Github来管理自己的代码和读书笔记][1]

测试是否能够连接：

    $ ssh -T git@github.com
关联远程仓库：

    $ git remote add origin git@github.com:TongxinV/xxx.git
取回远程主机origin某个分支的更新，再与本地的指定分支合并：

    $ git pull origin master


###正常的工作流程

> 配置都设置好了，且也不是第一次push

 1. 创建或修改文件
 2. 使用`git add`命令添加**新创建或修改的文件**到本地的缓存区（Index）
 3. 使用`git commit -m "注释"`命令将缓存区内容提交到**本地代码库**
 4. 使用`git push`命令将**本地代码库**同步到远端代码库


    使用git status命令查看当前git仓库的状态：
    . 文件处于untracked状态，需要git add命令将他们加入到缓存区（Index）
    . 使用git commit后再次使用git status，会发现当前的代码库已经没有待提交的文件，缓存区(Index)已经被清空


###错误:fatal: The current branch master has no upstream branch

> 当前分支master没有上游分支

分支第一次push会发生的错误

    git push --set-upstream origin master
    origin(表示远程仓库) 
    master(当前分支名称)


###错误：error: failed to push some refs to 'git@github.com:TongxinV/git_test.git'

> 不能推送

远程仓库里origin存在本地没有的文件，所以先`git pull origin master`下来（pull之后你的本地就会出现这个文件），再`git push`就可以了



###错误：fatal: refusing to merge unrelated histories

> 致命：拒绝合并无关的历史,即拒绝合并两个不相关的仓库

使用如下命令：

    git pull origin master --allow-unrelated-histories 








[1]:http://www.open-open.com/lib/view/open1423810370232.html
[2]:http://www.cnblogs.com/mengdd/p/3447464.html
