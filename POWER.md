---
name: "power-creator"
displayName: "Power 创建助手"
description: "快速创建 Kiro Power 骨架工程，自带版本管理和发布功能"
keywords:
  - "power"
  - "创建"
  - "create"
  - "scaffold"
  - "骨架"
  - "模板"
  - "template"
  - "版本"
  - "version"
  - "changelog"
  - "发布"
  - "release"
---

# Power 创建助手

帮助你快速创建 Kiro Power 骨架工程，包含完整的版本管理和发布功能。

## 何时激活

当用户讨论以下内容时激活此 Power：

- 创建新的 Power
- Power 项目结构
- Power 模板/骨架
- 版本号管理
- CHANGELOG 生成
- 发布流程

## Onboarding

### 步骤 1：检查环境

确保已安装 Node.js 和 pnpm：

```bash
node --version   # 需要 Node.js 14+
pnpm --version   # 需要 pnpm
```

如果未安装 pnpm：

```bash
npm install -g pnpm
```

### 步骤 2：创建新 Power

告诉 Kiro 你想创建的 Power 名称和功能，例如：

```
创建一个名为 "my-awesome-power" 的 Power，用于 XXX 功能
```

Kiro 会自动生成完整的骨架工程。

## Power 骨架结构

```
my-power/
├── POWER.md              # Power 配置和文档
├── README.md             # 项目说明
├── LICENSE               # MIT 许可证
├── package.json          # 版本管理配置
├── .versionrc.json       # CHANGELOG 配置
├── .gitignore            # Git 忽略规则
├── CHANGELOG.md          # 变更日志
└── steering/             # Steering 指导文件
    └── getting-started.md
```

## Steering 文件映射

| 任务场景 | Steering 文件 | 说明 |
| -------- | ------------- | ---- |
| 创建 Power | `steering/power-structure.md` | Power 结构规范 |
| 编写 POWER.md | `steering/power-config.md` | POWER.md 配置指南 |
| 提交代码 | `steering/commit-convention.md` | Conventional Commits 规范 |
| 发布版本 | `steering/version-release.md` | 版本发布工作流 |

## 快速命令

```bash
# 安装依赖
pnpm install

# 发布新版本（自动判断）
pnpm release

# 指定版本类型
pnpm release:patch   # 0.1.0 → 0.1.1
pnpm release:minor   # 0.1.0 → 0.2.0
pnpm release:major   # 0.1.0 → 1.0.0

# 首次发布
pnpm release:first

# 预览（不实际发布）
pnpm release -- --dry-run
```

## 创建 Power 示例

### 基础 Power

```
创建一个 Power：
- 名称：code-reviewer
- 功能：代码审查助手
- 关键词：review, 审查, code quality
```

### 带 MCP Server 的 Power

```
创建一个 Power：
- 名称：database-helper
- 功能：数据库操作助手
- 需要 MCP Server 支持
```

## 常见问题

### Q: 如何发布到 GitHub？

```bash
# 初始化 Git
git init
git add .
git commit -m "feat: initial release"

# 关联远程仓库
git remote add origin https://github.com/your-org/your-power.git
git push -u origin main
```

### Q: 如何让用户安装我的 Power？

用户可以通过 Kiro Powers 面板添加你的 GitHub 仓库地址。
