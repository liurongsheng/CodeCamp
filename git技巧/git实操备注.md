###多端提交导致冲突

错误代码：

    Please move or remove them before you can merge
    
如果你有的修改以及加入暂存区的话 

>git reset --hard && git clean -xdf

如果没有加入暂存区的话

>git checkout . && git clean -xdf


###Git各个状态之间转换指令总结

<img src="../img/git-lifecycle.png" />

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