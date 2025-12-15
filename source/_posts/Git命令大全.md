---
title: Git命令大全
tags: [Git]
categories: [运维]
cover: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTHXsy8FDyJpLBYS4Lncoq-_o6FO0__AYKydQ&s
---
# Git 命令整理 📚

## 🔗 远程仓库管理

### ➕ 添加上游仓库（便于同步更新）
```bash
git remote add upstream https://github.com/原作者/原仓库名.git
```

### 🔍 验证远程仓库配置
```bash
git remote -v
```

## 🔄 分支操作

### 📥 获取上游仓库最新更改
```bash
git fetch upstream
```

### 🌿 基于上游分支创建新分支
```bash
# 基于 main 分支
git checkout -b feature/你的功能描述 upstream/main

# 基于 develop 分支  
git checkout -b feature/你的功能描述 upstream/develop
```

### 📤 推送分支到你的 fork 仓库
```bash
git push -u origin feature/chat-integration
```

## 🗑️ 分支删除

### 🚫 删除远程分支
```bash
git push origin --delete develop
```

### 🗂️ 删除本地分支
```bash
# 安全删除（已合并）
git branch -d develop

# 强制删除（未合并）
git branch -D develop
```

## 💡 使用提示
- 使用 `git remote -v` 查看当前配置的远程仓库
- `-u` 参数设置上游跟踪分支，简化后续推送
- 删除分支前请确认分支内容已合并或不再需要
