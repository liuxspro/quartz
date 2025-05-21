---
title: Git 常用命令
date: 2024-01-20T22:33:14+08:00
tags:
  - Git
---
## Tag
```bash
# 查看有哪些 tag
git tag

# 创建轻量标签
git tag [tag name]

# 创建带附注的标签
git tag -a [tag name] -m 'note'

# 查看 tag 对应的版本号
git git show [tag name]

# 删除本地tag
git tag -d [tag name]

# 将 tag 推送到远程仓库
git push origin [tag name]

# 推送本地所有 tag （只推送tag）
git push --tags
```
## 分支
```bash
# 创建并切换到[branch-name]分支
git checkout -b [branch-name]

# 列出所有本地分支
git branch

# 切换到指定分支，并更新工作区
git checkout [branch-name]

# 合并指定分支到当前分支
git merge [branch]

# 删除分支
git branch -d [branch-name]

# 切换并拉取远程分支
git checkout -b dev origin/dev
```



> [!note] See Also:
> - [常用 Git 命令清单 - 阮一峰的网络日志](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)