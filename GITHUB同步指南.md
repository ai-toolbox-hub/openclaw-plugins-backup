# GitHub 同步配置与操作指南

## 🎯 项目信息

**项目名称**：OpenClaw 灾备与同步方案分析
**本地路径**：/Volumes/workspace/ObsidianData/11. 灾备/openclaw-plugin-rsync/
**目标仓库**：ai-toolbox-hub/openclaw-plugin-rsync

---

## 📋 同步方案

### 方案一：手动同步（推荐）

#### 1. 首先在 GitHub 上创建仓库
1. 访问 [GitHub](https://github.com/new)
2. 仓库名称：`openclaw-plugin-rsync`
3. 描述：OpenClaw 备份方案分析与改进方案
4. 许可证：MIT 或 Apache 2.0
5. 点击"Create repository"

#### 2. 配置本地仓库
```bash
cd "/Volumes/workspace/ObsidianData/11. 灾备/openclaw-plugin-rsync"

# 添加远程仓库
git remote add origin git@github.com:ai-toolbox-hub/openclaw-plugin-rsync.git

# 或使用 HTTPS（需要输入密码）
git remote add origin https://github.com/ai-toolbox-hub/openclaw-plugin-rsync.git
```

#### 3. 推送到 GitHub
```bash
# 推送到 main 分支
git push -u origin main
```

---

## 📜 GitHub Actions 自动化同步（高级方案）

### 1. 创建 GitHub Actions 配置文件

#### `.github/workflows/sync.yml`
```yaml
name: Auto Sync OpenClaw Rsync Plugin
on:
  schedule:
    - cron: '0 0 * * *'  # 每日自动同步
  push:
    branches: [ main ]
  workflow_dispatch:     # 手动触发

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Sync to Obsidian repo
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Configure git
        run: |
          git config user.name "GitHub Action"
          git config user.email "github-action@github.com"

      - name: Commit and push changes
        run: |
          if [ -n "$(git status --porcelain)" ]; then
            git add .
            git commit -m "Auto sync OpenClaw rsync plugin files"
            git push origin main --force
          fi
```

---

## 🛠️ 本地开发与同步脚本

### 开发流程
```bash
# 1. 创建功能分支
git checkout -b feature/new-analysis

# 2. 进行修改
# 编辑文档...

# 3. 提交更改
git add .
git commit -m "Add: 新功能说明"

# 4. 推送到远程
git push origin feature/new-analysis

# 5. 创建 Pull Request 进行合并
```

---

## 🔧 高级同步配置

### 使用 SSH 密钥的自动化同步

#### 1. 生成 SSH 密钥（如果没有）
```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

#### 2. 配置 SSH 代理
```bash
echo "Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519" >> ~/.ssh/config
```

#### 3. 定期同步脚本（crontab）
```bash
# 创建同步脚本 sync.sh
#!/bin/bash
cd "/Volumes/workspace/ObsidianData/11. 灾备/openclaw-plugin-rsync" || exit 1

# 拉取最新更改
git pull origin main

# 更新本地内容
# 这里可以添加自动更新逻辑

# 提交更改
git add .
git commit -m "Auto sync $(date '+%Y-%m-%d %H:%M:%S')"
git push origin main
```

#### 4. 设置定时任务
```bash
# 每日自动同步
0 0 * * * cd "/Volumes/workspace/ObsidianData/11. 灾备/openclaw-plugin-rsync" && /bin/bash sync.sh >> sync.log 2>&1
```

---

## 📊 项目监控与报告

### 同步状态检查
```bash
# 检查同步状态
cd "/Volumes/workspace/ObsidianData/11. 灾备/openclaw-plugin-rsync" && git remote -v && git status && echo "--- 同步日志 ---" && git log --oneline | head -5
```

### 本地与远程比较
```bash
# 比较本地与远程内容
cd "/Volumes/workspace/ObsidianData/11. 灾备/openclaw-plugin-rsync"
git fetch origin
git diff main..origin/main --stat
```

---

## 🎯 问题排查与解决方案

### 常见问题

#### 1. 权限不足
**问题**：`Permission denied (publickey)`
**解决**：
```bash
# 检查 SSH 代理状态
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

#### 2. 远程仓库未找到
**问题**：`Repository not found`
**解决**：
- 检查远程仓库 URL 是否正确
- 确认 GitHub 仓库已创建
- 检查权限配置

#### 3. 文件编码问题
**问题**：中文文件名在远程仓库显示异常
**解决**：
```bash
git config core.quotepath false
git config --global i18n.commitencoding utf-8
```

---

## 🏗️ 项目架构建议

### 文件组织
```
openclaw-plugin-rsync/
├── README.md              # 项目说明（建议添加）
├── 备份方案分析.md         # 主要分析文档
├── rsync-configuration.md # rsync 配置文档
├── case-study/            # 应用案例
├── performance/           # 性能测试数据
└── examples/             # 使用示例
```

### 分支策略
```
main            # 生产分支
develop         # 开发分支
feature/xxx      # 功能分支
hotfix/xxx      # 紧急修复分支
```

---

## 📈 长期维护计划

### 第一阶段（2024年 Q1）
- [x] 项目初始化与基础配置
- [x] 添加核心分析文档
- [ ] 创建项目说明文档
- [ ] 添加使用示例

### 第二阶段（2024年 Q2）
- [ ] 添加性能测试数据
- [ ] 创建应用案例
- [ ] 完善自动化同步

### 第三阶段（2024年 Q3）
- [ ] 添加对比分析
- [ ] 创建API文档
- [ ] 添加使用说明视频

---

## 🔄 同步说明

**项目已准备完毕！** 您可以按照以下步骤进行同步：

### 快速启动（推荐）
```bash
cd "/Volumes/workspace/ObsidianData/11. 灾备/openclaw-plugin-rsync"

# 在 GitHub 上创建仓库后执行：
git remote add origin git@github.com:ai-toolbox-hub/openclaw-plugin-rsync.git
git push -u origin main
```

**重要提示**：第一次同步需要在 GitHub 上创建对应的仓库。
