---
title: git指南
date: 2022-03-11 11:50:59
tags: 编程
categories:
- [工具应用]
---

### 常用命令
#### 常用流程
* git pull
* git add .; git add [filename]
* git commit -m ""; git commit --amend
* git push
* git status: 查看本次修改

#### stash
* git stash
* git stash save "我是暂存名称"
* git stash pop
* git stash list
* git stash clear
* git stash drop [stashId]: 删除某个暂存
* git stash apply [stashId]: 使用某个暂存

#### commit
* git reset --soft 想撤回到的commit：撤回commit
* git log: 查看commit 记录

#### dif
* git diff

### branch
* git branch -D [branchId]: 删除本地分支
* git checkout -b 分支名：切换，如没有，就新建然后切换
* 

### checkout
*  git checkout -b device_3-1-3_BRANCH origin/device_3-1-3_BRANCH: 拉取远程分支
