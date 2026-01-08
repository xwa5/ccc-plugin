# 发布指南

本文档说明如何将 `ccc-plugin` 发布为 Claude Code Plugin，供其他用户安装使用。

## 📋 发布前检查清单

### 1. 确保所有文件就绪

```bash
ccc-plugin/
├── .claude-plugin/
│   ├── plugin.json          ✅ 插件元数据
│   └── marketplace.json     ✅ Marketplace 配置
├── commands/
│   ├── install.md           ✅ /ccc-install 命令
│   └── status.md            ✅ /ccc-status 命令
├── skills/
│   └── baidu-ccc-helper/
│       └── SKILL.md         ✅ 智能助手
├── .gitignore               ✅ Git 忽略规则
├── README.md                ✅ 使用文档
└── PUBLISHING.md            ✅ 发布指南（本文件）
```

### 2. 本地测试

```bash
# 在 Claude Code 中添加本地 Marketplace
/plugin marketplace add /Users/mengxinliu/Documents/ccc-plugin

# 安装插件
/plugin install baidu-ccc@ccc-plugin

# 测试命令
/ccc-status

# 测试智能识别
# 在对话中输入："帮我安装团队的 Claude 配置"
```

## 🚀 发布方式

### 方式 1: GitHub 仓库发布（推荐）

```bash
# 创建 GitHub 仓库后
cd /Users/mengxinliu/Documents/ccc-plugin
git init
git add .
git commit -m "Initial commit: Baidu CCC Plugin v1.0.0"
git remote add origin https://github.com/<your-org>/ccc-plugin.git
git push -u origin main

# 创建标签
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

**用户安装方式**：
```bash
/plugin marketplace add <your-org>/ccc-plugin
/plugin install baidu-ccc@<your-org>-ccc-plugin
```

### 方式 2: 本地分享

```bash
# 打包
cd /Users/mengxinliu/Documents
zip -r ccc-plugin.zip ccc-plugin/

# 用户解压后
/plugin marketplace add ./ccc-plugin
/plugin install baidu-ccc@ccc-plugin
```

## 🔄 版本更新

1. 更新 `.claude-plugin/plugin.json` 和 `marketplace.json` 中的版本号
2. 提交并创建新标签
3. 用户运行 `/plugin marketplace update` 获取更新

## 📝 版本号规范

遵循 Semver：
- `1.0.0` → `1.0.1` - Bug 修复
- `1.0.1` → `1.1.0` - 新增功能
- `1.1.0` → `2.0.0` - 破坏性变更
