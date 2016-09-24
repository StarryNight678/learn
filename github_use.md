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




## clone仓库

    git clone git@github.com:michaelliao/bootstrap.git

## 推送
可以推送pull request给官方仓库来贡献代码。
