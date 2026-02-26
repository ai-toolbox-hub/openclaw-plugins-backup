# 贡献指南

欢迎参与 OpenClaw Plugins Backup 项目的开发！

## 📋 贡献流程

### 1. 提交 Issue

如果您发现问题或有改进建议，请先创建 Issue 进行讨论。

### 2. Fork 项目

1. 点击 GitHub 页面上的 "Fork" 按钮
2. 克隆您的 fork 到本地：
   ```bash
   git clone git@github.com:your-username/openclaw-plugins-backup.git
   cd openclaw-plugins-backup
   ```

### 3. 创建分支

```bash
git checkout -b feature/your-feature-name
```

分支命名规范：
- 功能开发：`feature/功能名称`
- 修复问题：`hotfix/问题描述`
- 文档更新：`docs/文档主题`

### 4. 开发和提交

```bash
# 进行修改
# ...

# 提交更改
git add .
git commit -m "Add: 功能描述"
```

提交信息规范：
- 使用中文或英文提交信息
- 格式：`类型: 简要描述`
- 类型包括：Add, Update, Fix, Remove, Docs, Refactor

### 5. 推送到远程仓库

```bash
git push origin feature/your-feature-name
```

### 6. 创建 Pull Request

1. 访问您的 fork 仓库页面
2. 点击 "New Pull Request" 按钮
3. 选择目标分支（通常是 main）
4. 填写 PR 标题和描述
5. 提交 PR

## 🎯 开发规范

### 文档规范

- 使用 Markdown 格式
- 保持文档结构清晰
- 代码示例使用正确的语法高亮
- 图片和其他资源放在合适的位置

### 代码规范（如有）

- 遵循 Python 或其他语言的标准规范
- 使用类型注解
- 添加适当的注释
- 保持代码简洁和可读性

### 测试规范

- 为新功能添加测试
- 确保所有现有测试通过
- 测试覆盖重要功能点

## 🔍 审核流程

1. PR 提交后，项目维护者会进行初步审查
2. 可能会要求修改或补充内容
3. 审查通过后会合并到 main 分支

## 📞 联系方式

如有问题，请通过以下方式联系：

- 创建 Issue
- 发送邮件
- 加入社区讨论

感谢您的贡献！
