# Git 操作

[官方介绍](https://git-scm.com/book/zh/v2)
SVN 是记录每一次版本变动的内容
Git 是将每个版本独立保存，看似消耗更多的空间，但在分支管理上带来了很多便利

---
## 初始化
git init

## 配置
```
git config user.name  "名字"
git config user.email "邮箱"
```
用户名可能无法唯一标识，所以需要配置邮箱地址作为唯一标识，并且有了联系的方式

需要查看配置的名字或者邮箱使用
```
git config user.name
git config user.email
```
## 添加和提交文件

git分为三个区
- 工作区 Working Directory
- 缓存区(暂存区) Stage(index)
- 版本库 Repositiry(HEAD)

工作区 git add --> 缓存区 --> git commit 版本库

git文件的三种状态
- 已修改 modified
- 已暂存 staged
- 已提交 committed

## 查看状态
```
git status
git status -u // 携带参数 -u 可显示未跟踪文件，文件级别的变化，默认为文件夹级别的变化
```
工作区 橙色提醒 untracked files

缓存区 绿色提醒 change to be committed

版本库 Your branch is ahead of 'origin/master' by 1 commit.

## .gitignore 文件的使用

标识不需要提交版本控制的文件
```
test.md // 忽略指定的文件
*.iml  // 忽略文件类型为iml一类的文件
out/   // 忽略指定文件夹

/.idea   // 过滤指定文件夹
/fd/*    // 忽略根目录下的 /fd/ 目录的全部内容；

!.gitignore    // 不忽略该文件
```
## 快照

每一次提交都叫一个快照，每一个快照都记录着当时文件的样子
需要查看某个版本的代码，就取那个版本的快照。

## 日志
git log
```
C:\gitHub\CodeCamp>git log
commit acfeb84d3851a6002975df0e02914d01e65599dc (HEAD -> master, origin/master, origin/HEAD)
Author: liurongsheng <308837162@qq.com>
Date:   Fri Nov 9 19:58:36 2018 +0800
```
commit 后面的一长串数字是提交码，日志的显示是倒叙的形式
```
git log -1     // 显示最近的一次提交，后面的数字表示具体的次数
git log --oneline     // log记录比较多的时候，使用 oneline 参数可以一行显示一个记录
git log -1 -p     // p 参数显示修改的具体文件内容
```

gitk // git log 的图形化界面

master 分支，master可以理解为一个指针，指向最新的提交

HEAD 标签，指向当前的分支

## 差异比较

工作区 <- git diff -> 缓存区 <- git diff --cached -> 版本库

工作区 <- git diff HEAD -> 版本库

git diff d // 查看工作区和缓存区 d 文件的区别

## 取出历史版本
```
工作区 <- git checkout 缓存区 <- git checkout HEAD 版本库
                      工作区 <- git checkout HEAD 版本库
```
git checkout HEAD 命令会把缓存区和工作区的代码同时覆盖

git checkout 文件名    // 重置当前的工作区指定文件，内容版本为缓存区的版本 例如： git checkout .gitignore

git checkout .     // 重置当前的工作区，内容版本为缓存区的版本

git checkout HEAD .     // 重置当前的工作区和缓存区，内容版本为版本库的版本，特别注意缓存区也会被重置

git checkout 还有其他参数 比如 -m, --merge

使用 git checkout -help 查看具体指令

## 分支

列出分支

git branch

创建一个新的分支

git branch (branch-name)

删除一个分支

git branch -d (branch-name)

删除 remote 的分支

git push (remote-name) :(remote-branch)

实用场景：

代码开发到一定阶段可以上稳定版本，这时仍然需要开发新功能，但是这时也需要保持稳定版本不变。
创建开发分支 dev, 并切换到开发分支，这时可以提交代码到开发分支。

稳定版本上线后发现问题，需要修复 bug，我们把代码切换到主干的稳定版本master 分支，在新建一个稳定版本的 bugfix 分支，修改 bug
等待测试回归 bug ，确认解决后，切换到稳定版本 master 分支，合并 bugfix 分支
```
git branch dev // 创建 dev 分支
git branch // 查看分支
git checkout dev // 切换到 dev 分支

C:\gitHub\init>git log --oneline
65be6bb (HEAD -> dev, master) C3
8238627 C2
501e024 C1

git add .
git commit -m "C4"

C:\gitHub\init>git log --oneline
18e5097 (HEAD -> dev) C4
65be6bb (master) C3
8238627 C2
501e024 C1
// 提交 dev 分支代码
---
// 切换到 稳定版本 master 分支
git checkout master

C:\gitHub\init>git log --oneline
65be6bb (HEAD -> master) C3
8238627 C2
501e024 C1

git checkout -b bugfix  // 创建并切换到分支 bugfix

C:\gitHub\init>git branch
* bugfix
  dev
  master

git add .
git commit -m "C5"

// 提交 bug 修复的代码

C:\gitHub\init>git log --oneline
8dc397e (HEAD -> bugfix) C5
65be6bb (master) C3
8238627 C2
501e024 C1

C:\gitHub\init>git branch -v
* bugfix 8dc397e C5
  dev    18e5097 C4
  master 65be6bb C3
---
// 把 bugfix 分支整合到 master 分支

git checkout master

C:\gitHub\init>git merge bugfix
Updating 65be6bb..8dc397e
Fast-forward
 c5.md | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 c5.md

C:\gitHub\init>git branch -v
  bugfix 8dc397e C5
  dev    18e5097 C4
* master 8dc397e C5
---
// 合并完成删除 bugfix 分支
git branch -d bugfix

C:\gitHub\init>git branch -v
  dev    18e5097 C4
* master 8dc397e C5

// 切换到 dev 分支继续开发
git chenkout dev

git add .
git commit -m "C6"

C:\gitHub\init>git log --oneline
73cbad6 (HEAD -> dev) C6
18e5097 C4
65be6bb C3
8238627 C2
501e024 C1

// 新开发的功能稳定了，准备整合 dev 分支

git checkout master

C:\gitHub\init>git log --oneline
8dc397e (HEAD -> master) C5
65be6bb C3
8238627 C2
501e024 C1

git merge dev

C:\gitHub\init>git log --oneline
608f7a7 (HEAD -> master) Merge branch 'dev'
73cbad6 (dev) C6
8dc397e C5
18e5097 C4
65be6bb C3
8238627 C2
501e024 C1
---
// 模拟冲突的情况
git checkout dev
git merge master
git add .
git commit -m "change on dev"
C:\gitHub\init>git log --oneline
ed7d77c (HEAD -> dev) change on dev
73cbad6 C6
18e5097 C4
65be6bb C3
8238627 C2
501e024 C1

git checkout master

// 修改和开发上一步修改的同一个文件制造冲突
// 同样提交版本
git add .
git commit -m "change on master"

C:\gitHub\init>git log --oneline
dfe64c3 (HEAD -> master) change on master
608f7a7 Merge branch 'dev'
73cbad6 C6
8dc397e C5
18e5097 C4
65be6bb C3
8238627 C2
501e024 C1

// 现在合并 dev 分支
git merge dev

C:\gitHub\init>git merge dev
Auto-merging c4.md
CONFLICT (content): Merge conflict in c4.md
Automatic merge failed; fix conflicts and then commit the result.

// 这里会出现冲突文件，需要修改合并代码提示的冲突文件
<<<<<<< HEAD
C4 change on mater
=======
C4 change on dev
>>>>>>> dev

// 修改冲突的文件，然后再次 git commit -m "merge dev" 完成合并

C:\gitHub\init>git log --oneline
99670d1 (HEAD -> master) merge dev
dfe64c3 change on master
ed7d77c (dev) change on dev
608f7a7 Merge branch 'dev'
73cbad6 C6
8dc397e C5
18e5097 C4
65be6bb C3
8238627 C2
501e024 C1
```

## 快进的概念
旧版本能一步到达新的版本的就是可以快进，如果不能快进则 git 会自动创建新的提交进行合并

## 使用 git stash 暂存未提交的修改

实际场景，在工作暂时做了一部分，需要切换到别的分支，需要暂存当前的修改。

- git stash //把所有没有提交的修改暂存到stash里面，使用了这条命令后，未提交的内容会消失

- git stash save <message> //给 stash 存储的修改起个名字

- git stash list //查看暂存区的所有暂存修改
```
C:\gitHub\init>git stash list
stash@{0}: WIP on master: 99670d1 merge dev
// WIP, Work In Progess的简称，说明代表了工作区进度。 
// Index, 代表的是已经被 add 但是还未被提交的进度。
```
如果是当前的可以直接使用

- git stash apply 来取出暂存

- git stash apply stash@{X} //取出相应的序列的暂存

- git stash pop  //取出最近一次暂存并删除记录列表中对应记录

- git stash drop stash@{X} //将记录列表中取出的对应暂存记录删除

- git stash clear 清空stash队列

## 获取远程仓库

git clone [url]

例：git clone https://github.com/you/yourpro.git

## 创建远程仓库

添加一个新的 remote 远程仓库
- git remote add [remote-name] [url]

例：git remote add origin https://github.com/you/yourpro.git

origin：相当于该远程仓库的别名
    
列出所有 remote 的别名
- git remote
    
列出所有 remote 的 url
- git remote -v
    
删除一个 remote
- git remote rm [name]
    
重命名 remote
- git remote rename [old-name] [new-name]

## 从本地仓库中删除

- git rm file.txt         // 从版本库中移除，删除文件
- git rm file.txt -cached // 从版本库中移除，不删除原始文件
- git rm -r xxx           // 从版本库中删除指定文件夹

## 从本地仓库中添加新的文件

- git add .               // 添加所有文件
- git add file.txt        // 添加指定文件

## 提交，把缓存内容提交到 HEAD 里

- git commit -m "注释"

## 撤销

撤销最近的一个提交.
- git revert HEAD

取消 commit + add
- git reset --mixed

取消 commit
- git reset --soft

取消 commit + add + local working
- git reset --hard

## 把本地提交 push 到远程服务器

git push [remote-name] [loca-branch]:[remote-branch]
例：git push origin master:master

    
### 从远程库中下载新的改动

git fetch [remote-name]/[branch]

### 合并下载的改动到分支

git merge [remote-name]/[branch]

### 从远程库中下载新的改动

pull = fetch + merge
git pull [remote-name] [branch]
例：git pull origin master

### 切换分支

切换到一个分支
git checkout [branch-name]

创建并切换到该分支
git checkout -b [branch-name]
    
### 分支合并到主干
    
首先把分支的代码先提交 git add . && git commit -m "change" && git push
然后切换到主干 git checkout master
合并 git merge origin/index-swiper
提交 git push
主干包含所有的功能最新的代码，分支是开发新功能的具体代码，测试没有问题后提交到主干
    
### 与github建立ssh通信，让Git操作免去输入密码的繁琐。
    
首先呢，我们先建立ssh密匙。
> ssh key must begin with 'ssh-ed25519', 'ssh-rsa', 'ssh-dss', 'ecdsa-sha2-nistp256', 'ecdsa-sha2-nistp384', or 'ecdsa-sha2-nistp521'.  -- from github

根据以上文段我们可以知道github所支持的ssh密匙类型，这里我们创建ssh-rsa密匙。
在command line 中输入以下指令:``ssh-keygen -t rsa``去创建一个ssh-rsa密匙。
如果你并不需要为你的密匙创建密码和修改名字，那么就一路回车就OK，

>$ ssh-keygen -t rsa

Generating public/private rsa key pair.
//您可以根据括号中的路径来判断你的.ssh文件放在了什么地方
Enter file in which to save the key (/c/Users/Liang Guan Quan/.ssh/id_rsa):

* 到 https://github.com/settings/keys 这个地址中去添加一个新的SSH key，然后把你的xx.pub文件下的内容文本都复制到Key文本域中，然后就可以提交了。
* 添加完成之后 我们用``ssh git@github.com`` 命令来连通一下github，如果你在response里面看到了你github账号名，那么就说明配置成功了。 
 
---

在gitolite-admin的conf文件夹下修改gitolite.conf添加项目名

在项目中初始化项目 git init
```
git add .
git commit -m "init"
git remote add origin git@192.168.90.51:myApp.git
git push origin master:master

git checkout -b newBranch 创建分支
```
如果是在gitHub上创建了项目，这个时候没有文件。在本地初始化后打算提交到gitHub，
由于版本冲突不能push成功，使用`git push -f` 可以强推成功，但是gitHub上的初始化文件会消失，比如README.md文件
