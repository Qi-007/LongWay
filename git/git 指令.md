# git 指令

## 一、git介绍
Git 是一种分布式版本控制系统，它可以记录代码的变更历史和版本，并能够协调多个开发者对同一代码库的修改，以保证代码变化的连续性和协作开发的顺畅性。

## 二、Git 基本概念：
仓库（Repository）：存储代码的地方，可以是本地的，也可以是远程的。

提交（Commit）：将代码快照保存在仓库中，记录了代码的变化历史。

分支（Branch）：代码的一个独立分支，用于同时进行多个开发任务，不会影响主分支代码。

合并（Merge）：将两个分支的代码合并成一个。

拉取（Pull）：获取远程仓库的最新代码。

推送（Push）：将本地仓库中的提交推送到远程仓库中。

## 三、Git初始化操作命令
配置用户名
git config --global user.name “填你的名字”
配置邮箱
git config --global user.email 130@qq.com

**ps:** 可以使用SSH密钥避免每次连接时都要输入密码

## 四、 Git 基本流程(从0-1步骤)：
安装后：

1.  查看版本：git --version

2. 配置用户名：git config --global user,name “***”

3. 配置邮箱：git config --global user.email ***

4. 初始化一个新的Git仓库：git init

5. 登录gitee复制仓库地址

![git](picture/git.png)

6. 和远程仓库建立连接：git remote add orlgin https://gitee.com/****.git

7. 把远程分支拉到本地git fetch origin dev（master）（dev/master为远程仓库的分支名）

8. 本地创建分支并切换到该分支git checkout -b dev origin/develop
   ————————————————

## 五、常见命令

1. git init

初始化一个新的Git仓库。

这将在当前目录中创建一个名为".git"的子目录，Git会将所有仓库的元数据存储在其中。

作用:用于初始化一个新的Git仓库。执行这个命令后，Git会在当前目录下创建一个名为".git"的子目录，其中存储着仓库的所有元数据。

2. git clone

克隆一个已存在的仓库。
这会创建一个本地仓库的副本，包括其所有的历史记录和分支。

git clone <仓库链接>

3. git add

将修改内容添加到下一次提交中。
这将把指定的文件添加到暂存区，这些文件将包含在下一次提交中。

git add file1.txt file2.txt

4. git commit

创建一个新的提交。
这将记录暂存区的修改以及自上次提交以来所做的任何其他修改，并附带一条描述这些修改的提交信息。

git commit -m "添加新功能"

5. git push

将提交推送到远程仓库。
这将把本地的提交发送到指定的远程仓库，更新远程分支以包含新的提交。

git push origin main

6. git pull

从远程仓库获取并合并修改。
这会从指定的远程仓库中获取最新的提交，并将其合并到当前分支中。

git pull origin main

7. git remote

关联远程仓库，和远程仓库建立连接。

git remote add orlgin https://gitee.com/****.git

8. git branch

列出、创建或删除分支。
这个命令可以用来列出仓库中可用的分支，创建新的分支或删除现有的分支。

git branch new-branch
分支删除

git branch -d <分支名>

9. git checkout

切换到不同的分支。
这个命令允许你切换到仓库中的不同分支，并将其作为当前工作分支。

git checkout main

10. git merge

将一个分支合并到另一个分支。
这个命令将一个分支的修改合并到另一个分支中，创建一个反映合并变化的新提交。

git merge new-branch

11. git status

显示仓库的状态。
这个命令会显示当前分支、任何暂存或未暂存的修改以及任何未跟踪的文件。

git status

12. git rebase

将一个分支的修改合并到另一个分支。
假设你在"XYZ"分支上进行了一些修改，你希望将这些修改合并到"main"分支中。你可以使用git rebase命令将你的修改重新应用到main分支之上。

13. git revert
    应用场景：有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了，需要撤销它。
    你可以使用git revert创建一个新的提交，该提交会撤销之前提交引入的修改。

git revert <commit1>..<commit2>

14. git .gitignore
    使用方式：

告诉 Git 忽略所有以 .o 或 .a 结尾的文件:*.[oa]
告诉 Git 忽略所有名字以波浪符（~）结尾的文件 文件：* ~
1忽略所有的 .a 文件
2但跟踪所有的 lib.a，即便你在前面忽略了 .a 文件
3忽略 doc/ 目录及其所有子目录下的 .pdf 文件

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。

原文链接：https://blog.csdn.net/weixin_43710744/article/details/134221849
