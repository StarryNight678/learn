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
## 使用命令

- 设置用户和email

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
- 通过git init命令把这个目录变成Git可以管理的仓库：

```
    $ git init
```
让git显示颜色

    git config --global color.ui true

## 提交
- 添加文件

```
    git add readme.txt
```
- 用命令git commit告诉Git，把文件提交到仓库：


    $ git commit -m "wrote a readme file"    

- 查看状态


    git status

- 历史记录

    git log

- 显示具体修改

```
    $ git diff
    diff --git a/r.txt b/r.txt
    index e69de29..6f1a89a 100644
    --- a/r.txt
    +++ b/r.txt
    @@ -0,0 +1 @@
    +jdsfja
    warning: LF will be replaced by CRLF in r.txt.
    The file will have its original line endings in your working directory.
```
-  版本回退

```
     git reset --hard HEAD
     回退到指定版本
     git reset --hard 3628164
```

- 用来记录你的每一次命令,**这里可以查到回退的版本号**

```
    $ git reflog
    1a7510f HEAD@{0}: commit: test
    acc549e HEAD@{1}: commit: git use
    228e176 HEAD@{2}: commit: learn git
    d3dd118 HEAD@{3}: clone: from
```
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

## 远程仓库
git杀手级功能之一

[使用github远程仓库](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001374385852170d9c7adf13c30429b9660d0eb689dd43a000)

- 关联远端仓库

```
    git remote add origin git@github.com:username/learngit.git
```
- 本地内容推送

```
    git push -u origin master
```
    git push命令，实际上是把当前分支master推送到远程
    从现在起，只要本地作了提交，就可以通过命令：
把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

```
    git push origin master
```

- 小结


要关联一个远程库，使用命令`git remote add origin` git@server-name:path/repo-name.git；

关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；


## clone仓库

```
    $ git clone git@github.com:michaelliao/gitskills.git
```
克隆到本地

## 分支管理
分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

其他版本控制系统如SVN等都有分支管理，但是用过之后你会发现，这些版本控制系统创建和切换分支比蜗牛还慢，简直让人无法忍受，结果分支功能成了摆设，大家都不去用。

但Git的分支是与众不同的，无论创建、切换和删除分支，Git在1秒钟之内就能完成！无论你的版本库是1个文件还是1万个文件。

1. 创建和合并分支

[分支创建和合并的原理](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000)

创建分支并切换
```
git checkout -b dev
```
git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：

$ git branch dev
$ git checkout dev

查看当前分支
```
git branch
```
git branch命令会列出所有分支，当前分支前面会标一个*号。

切换分支
```
git checkout master
```

合并分支
```
git merge dev
```

合并完成后，就可以放心地删除dev分支了：
```
$ git branch -d dev
```

小结
Git鼓励大量使用分支：

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>


## 解决冲突

需要先解决冲突然后合并

查看合并的图形表示
```
    git log --graph
```

分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

所以，团队合作的分支看起来就像这样：
![分支合并](http://www.liaoxuefeng.com/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0)


## Bug分支
Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：


    $ git stash
现在，用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。

当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它


- 恢复工作现场

```
git stash list
```

1. `git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

2. 用`git stash pop`，恢复的同时把stash内容也删了

强行删除分支
````
git branch -D feature-vulcan
````

## 多人协作
远程仓库的默认名称是origin。
要查看远程库的信息，用`git remote`

    $ git remote

1. 首先，可以试图用git push origin branch-name推送自己的修改；

1. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

1. 如果合并有冲突，则解决冲突，并在本地提交；

1. 没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

## 标签管理
    $git tag v1.0

对历史提交打tag

    $ git tag v0.9 6224937

查看标签

     $git tag

查看标签提交

    git show v1.0

## 小结
命令`git tag <name>`用于新建一个标签，默认为HEAD，也可以指定一个commit id；

`git tag -a <tagname> -m "blablabla...`可以指定标签信息；

`git tag -s <tagname> -m "blablabla...`可以用PGP签名标签；

命令git tag可以查看所有标签。


## 搭建git服务器

[搭建git服务器教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137583770360579bc4b458f044ce7afed3df579123eca000)

- 小结

搭建Git服务器非常简单，通常10分钟即可完成；

要方便管理公钥，用Gitosis；

要像SVN那样变态地控制权限，用Gitolite


## 总结

Git虽然极其强大，命令繁多，但常用的就那么十来个，掌握好这十几个常用命令，你已经可以得心应手地使用Git了。

友情附赠国外网友制作的Git Cheat Sheet，建议打印出来备用：

[Git Cheat Sheet](https://pan.baidu.com/s/1kU5OCOB#path=%252Fpub%252Fgit)


## 参考

本文通过学习[Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
学习git提高效率












