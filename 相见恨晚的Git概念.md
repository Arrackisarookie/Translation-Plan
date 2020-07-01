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
