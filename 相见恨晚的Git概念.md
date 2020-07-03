# 相见恨晚的 Git 概念

原文链接：[Git Concepts I Wish I Knew Years Ago](https://dev.to/g_abud/advanced-git-reference-1o9j)

我辈开发者使用最多的技术既不是 JavaScript，
也不是 Python 或者 HTML。
它甚至在面试中都很少被提到，也很少被列入工作的必备技术栈。

没错，我说的正是 Git 和版本控制。

长久以来，我们大部分开发人员只学过一点点 Git 的概念。
这些知识仅仅能让我们拥有在一个小团队内使用简单功能分支工作流的能力。
如果你也像我一样，这种状态将会伴随你的职业生涯很久。

是时候再访 Git，重新审视一下掌握它对我们职业生涯的提升有多么重要。
本指南可以作为一篇参考，它包含了一些我认为很是重要但可能鲜为人知的概念。
掌握 Git 之后，你管理代码的方式以及每天的工作流将会发生巨大的改变。
由于 Git 命令有些陈旧并且难以记忆，因此本文将会按照概念和预期表现进行分解。

如果你对 Git 的基本概念掌握的不够牢固，比如工作目录、本地仓库和远程仓库之间的区别，
那么建议你可以先阅读[这篇指南](https://dev.to/unseenwizzard/learn-git-concepts-not-commands-4gjc)。
同样，如果没有掌握 Git 的基本命令，可以从[官方文档](https://git-scm.com/docs/gittutorial)开始学习。
本文并不意味着会带你从一个彻底的新手变成专业人员，
而是默认你已经熟练掌握如何使用 Git。

## 目录

- Git 命令
    + 日志 (Logging)
    + 导航 (Navigation)
    + 修改 (Modifications)
    + 清理 (Cleanup)
    + 别名 (Aliases)
- 其他 Git 技巧
    + 忽视文件 (Ignoring Files)
    + 特殊文件 (Special Files)
- Git 工作流
    + Rebase vs. Merge
    + 远程仓库设置 (Remote Repository Setting)
    + 分支命名 (Branch Naming)
    + 提交信息 (Commit Messages)

## Git 命令

### 日志 (Logging)

#### 我刚干哈了
``` shell
$ git log
$ git log --oneline  # 更为精炼的输出
$ git log --graph  #  以分支的可视化图显示
```

#### 查看你的撤销历史
``` shell
$ git reflag
```
因为有时 `git log` 命令无法捕捉到撤销的命令，
特别是对于那些无法在 commit 历史里显示的命令。

在你运行了类似 `git rebase` 这样的“危害型”命令后，
`reflag`  基本上可以算是一层安全网。
你不仅可以看到之前所做的 commit，
而且还将看到导致 commit 的每一个过程。
看这篇 [Atlassian 上的文章](https://www.atlassian.com/git/tutorials/refs-and-the-reflog)
来了解更多关于 refs 运作方式。

#### 查看当前状态 + 任何合并冲突
``` shell
$ git status
```
虽然 `git status` 是一个非常基础的命令，我们很早之前就学过，
但是，由于它作为 Git 内部基本原理的学习工具，其重要程度仍然值得
我们重复学习。
它还可以帮助你浏览复杂的 rebase 和 merge 过程。

#### 对比 staged (或者 unstaged) 中的异同
``` shell
$ git diff --staged  # staged 的改变
$ git diff   # unstaged 的改变
```

#### 对比两个分支之间的异同
``` shell
$ git diff branch1..branch2
```

### 导航 (Navigation)
#### 我想看看我之前干哈了
``` shell
$ git reset <commit-sha>
```
这条命令将会撤销对应 commit，并且取消那次 commit 中的 stage 操作，
但是那些文件仍然保留在工作目录。

#### 我想切换到别的分支
``` shell
$ git switch branch-name  # Git 2.23 中的新语法
$ git checkout branch-name  # 经典语法
```
`git checkout` 可能会有些让人难以理解，因为他既可以工作在文件层级，
也可以工作在分支层级。
从 [Git 2.23](https://www.infoq.com/news/2019/08/git-2-23-switch-restore/)
开始，我们拥有了两个新的命令：

- `git restore` 用来 checkout 文件
- `git switch` 用来 checkout 分支

如果你想避免 `git checkout` 造成的困扰，上面两个命令非常适合你。

#### 我想回到之前我在的分支
``` shell
$ git switch -
```

### 修改 (Modifications)
#### 我把自己挖进了兔子洞，让我们重新开始
(译者注: get 不到这个梗。。)

``` shell
$ git reset --hard HEAD
```
这条命令将重置本地目录到最近一次 commit 的状态，并且会放弃所有 unstage 的文件。

#### 我想把一个文件重置到之前的样子
``` shell
$ git restore <filename>  # Git 2.23 新语法
$ git checkout -- <filename>  # 经典语法
```
#### 我想撤销上一次 commit 并且重写历史
``` shell
$ git reset --hard HEAD~1
```
#### 我想回到 n 次 commit 之前
``` shell
$ git reset --hard HEAD~n  # 回到倒数第 n 次 commit
$ git reset --hard <commit-sha>  # 或者回到特定的某次提交
```
`soft`，`mixed` 和 `hard` 三种 reset 的不同：

- `--soft`：撤销 commit 但是工作目录中会保留更改
- `--mixed` (默认)：撤销 commit，撤销当次 commit 的 stage，但是工作目录中会保留更改
- `--hard`：撤销 commit，撤销当次 commit 的 stage，并且删除更改

#### 
