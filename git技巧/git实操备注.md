# git 实操备注

## 多端提交导致冲突

错误代码：

    Please move or remove them before you can merge

如果你有的修改以及加入暂存区的话

> git reset --hard && git clean -xdf

如果没有加入暂存区的话

> git checkout . && git clean -xdf

## Git 各个状态之间转换指令总结

<img src="../img/git-lifecycle.png" alt="git状态之间转换指令" />

基本状态标识

    A- = untracked 未跟踪
    A = tracked 已跟踪未修改
    A+ = modified - 已修改未暂存
    B = staged - 已暂存未提交
    C = committed - 已提交未PUSH

各状态之间变化

    A- -> B : git add <FILE>
    B -> A- : git rm --cached <FILE>
    B -> 删除不保留文件 : git rm -f <FILE>
    A -> A- : git rm --cached <FILE>
    A -> A+ : 修改文件
    A+ -> A : git checkout -- <FILE>
    A+ -> B : git add <FILE>
    B -> A+ : git reset HEAD <FILE>
    B -> C : git commit
    C -> B : git reset --soft HEAD^
    修改最后一次提交:git commit --amend

## git 高级操作

`git reflog` 查看本地记录

### 恢复最近一次 commit

`git reset --soft HEAD^`

`git reset --soft HEAD~1` 撤销一个 commit 未 push 的情况，相当于 webStorm 中的撤销提交

`git reset --soft HEAD~2` 撤销两个 commit 未 push 的情况

`git reset --hard xxxx` 这个操作不会取消 rebase 状态，如果 rebase 没有完成 HEAD 指向会有感叹号

### cherry-pick --continue

git log 查找到需要 pick 出来的提交 commitId
`git cherry-pick commitId`

支持多个
`git cherry-pick commitId1 commitId2`

支持区间 (commitId1、commitId2)
`git cherry-pick commitId1^..commitId2`

多个 pick 的时候遇到冲突的话 `cherry-pick --continue` 继续流程

放弃 pick 操作，就跟什么都没有操作过一样
`gits cherry-pick --abort`

放弃 pick 操作，应用当前的进度
`git cherry-pick --quit`

### revert 掉自己提交的

方法一：比直接 revert 要好一些，采用 `--soft` 模式会保留本地代码的变化，`--hard` 则不会

- `git log` // 查到需要回退的那个提交的 commitId
- `git reset --soft commitId` // commitId 为前面找到的 commitId，本地还原到这个提交的内容
- `git push origin 分支名 --force` // 分支名，就选当前的分支，再次提交后就清空了

方法二：`git revert commitId`
revert 会生成一条新的提交记录，这时会让你编辑提交信息，编辑完后 :wq 保存退出就好了

### 还原 rebase 操作，取消 rebase 状态

`git rebase --abort` 这个操作会让未完成的 rebase 操作的 HEAD 感叹号消失

`git merge --squash develop` 要合并提交的目标分支

### 忽略本地的变更，比如 .env 文件

git update-index --assume-unchanged public/app.config.js

### GitHub 额外教程

在 GitHub 上，直接修改 URL 就可以让用户以多种形式查看差别

1. 查看 4-0-stable 分支与 3-2-stable 分支之间的差别
   <https://github.com/rails/rails/compare/4-0-stable...3-2-stable>

1. 查看与几天前的差别
   <https://github.com/rails/rails/compare/master@{7.day.ago}...master>

1. 查看与指定日期之间的差别，查看 master 分支 2013 年 1 月 1 日与现在的区别
   <https://github.com/rails/rails/compare/master@{2013-01-01}...master>

1. 获取 diff 格式的文件，只要像下面这样在 URL 末尾添加 .diff 即可
   <https://github.com/用户名/仓库名/pull/28.diff>
   同理， 想要 patch 格式的文件， 只需要在 URL 末尾添加 .patch 即可
   <https://github.com/用户名/仓库名/pull/28.patch>

### 线上文档

<http://git-scm.com/book/zh/v2>

<https://learngitbranching.js.org/?demo=&locale=zh_CN>

### 名词备注

- 冲突（Conflict）
- git reflog 命令，查看当前仓库执行过的操作的日志
- git reset --hard 目标时间点的哈希值，可以完全恢复至该时间点的状态，哈希值只要输入 4 位以上就可以执行
- git init——初始化仓库
- git status——查看仓库的状态
- git add——向暂存区（Stage 或者 Index）中添加文件
- git commit——保存仓库的历史记录
- git log——查看提交日志
- git log --pretty=short 只想让程序显示第一行简述信息
- git diff 命令，查看当前工作树与暂存区的差别
- git branch——显示分支一览表
- git checkout -b——创建、切换分支，- b 参数的后面是本地仓库中新建分支的名称
- 特性（Topic）
- git merge——合并分支
- git log --graph——以图表形式查看分支
- 冲突部分，======= 以上的部分是当前 HEAD 的内容，以下的部分是要合并的分支中的内容
- git commit --amend——修改上一条提交信息
- git rebase -i——压缩历史
- git remote add——添加远程仓库
- git remote add origin <git@github.com>:github-book/git-tutorial.git
- git push——推送至远程仓库，
- git push -u origin feature-D， -u 参数可以在推送的同时，将 origin 仓库的 master 分
  支设置为本地仓库当前分支的 upstream（上游）
- git clone——获取远程仓库
- git pull——获取最新的远程仓库分支
- 管理 Issue 的系统称为 BTS(Bug Tracking System，BUG 跟踪系统)。
- 代表性的 BTS 有 RedmineA、TracB、Bugzilla
- `http://www.redmine.org/` `http://trac.edgewall.org/` `http://www.bugzilla.org/`

- git gc, 用于清理不必要的文件和优化本地存储库的命令
- git prune, 用于清理孤立或无法访问的 Git 对象的命令

## 本月要做的任务

- [ ] 完成图片
- [x] 完成部署工具的设置
- [ ] 实现抽签功能

## 提交类型模板

- New feature
- Bug fix
- Site / documentation update
- Demo update
- Component style update
- TypeScript definition update
- Bundle size optimization
- Performance optimization
- Enhancement feature
- Internationalization
- Refactoring
- Code style optimization
- Test Case
- Branch merge
- Other (about what?)
