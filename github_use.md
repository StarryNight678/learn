# github使用

![1](http://www.liaoxuefeng.com/files/attachments/0013848605496402772ffdb6ab448deb7eef7baa124171b000/0)

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。

## 集中式和分布式


集中式版本控制系统最大的毛病就是必须联网才能工作
分布式:
- 安全性高,个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧
- 多人修改同一个文件,只需把各自的修改推送给对方，就可以互相看到对方的修改了。
- 交流修改的“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已。

集中式 cvs最早,svn修正了cvs的问题,用的最多的集中式版本控制软件

微软集中式版本控制系统叫VSS，集成在Visual Studio中。由于其反人类的设计，连微软自己都不好意思用了。
# 使用命令

- 设置用户和email


    $ git config --global user.name "Your Name"
    $ git config --global user.email "email@example.com"

- 通过git init命令把这个目录变成Git可以管理的仓库：


    $ git init

## 提交
- 添加文件


    git add readme.txt
- 用命令git commit告诉Git，把文件提交到仓库：


    $ git commit -m "wrote a readme file"    

- 查看状态


    git status

- 历史记录


    git log

- 显示具体修改


    $ git diff
    diff --git a/r.txt b/r.txt
    index e69de29..6f1a89a 100644
    --- a/r.txt
    +++ b/r.txt
    @@ -0,0 +1 @@
    +jdsfja
    warning: LF will be replaced by CRLF in r.txt.
    The file will have its original line endings in your working directory.

-  版本回退


     git reset --hard HEAD
    #回退到指定版本
     git reset --hard 3628164

- 用来记录你的每一次命令,**这里可以查到回退的版本号**


    $ git reflog
    1a7510f HEAD@{0}: commit: test
    acc549e HEAD@{1}: commit: git use
    228e176 HEAD@{2}: commit: learn git
    d3dd118 HEAD@{3}: clone: from

现在总结一下：
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

## 工作区和暂存区

工作区（Working Directory）就是你在电脑里能看到的目录
版本库（Repository）,工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。Git的版本库里存了很多东西，其中最重要的就是称为**stage**（或者叫**index**）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。


git add  先把修改提交到暂存区,commit提交到master中

## 管理修改
Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。

## 撤销修改
```
git checkout -- readme.txt
```
命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

1. readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
1. readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。

**注意**

git checkout -- file命令中的``--``很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。

- 小结

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

## 删除文件
直接删,然后提交
一是确实要从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`

# 远程仓库
git杀手级功能之一
jjjj


## clone仓库

    git clone git@github.com:michaelliao/bootstrap.git

## 推送
可以推送pull request给官方仓库来贡献代码。
