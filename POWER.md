---
name: "power-creator"
displayName: "Power 创建助手"
description: "快速创建 Kiro Power 骨架工程，包含完整的开发环境和自动化发布流程"
keywords:
  - "power"
  - "创建"
  - "create"
  - "scaffold"
  - "骨架"
  - "模板"
  - "template"
  - "新建"
  - "初始化"
  - "init"
---

# Power 创建助手

帮助你快速创建完整的 Kiro Power 开发骨架，包含：

- 📁 标准目录结构
- 🔄 dev/main 双分支工作流
- 📦 自动化版本管理
- 🚀 一键发布到 GitHub

## 何时激活

当用户讨论以下内容时激活此 Power：

- 创建新的 Power
- 初始化 Power 项目
- Power 项目结构
- Power 模板/骨架

## Onboarding

### 步骤 1：告诉我你的 Power 信息

```
创建一个 Power：
- 名称：my-awesome-power
- 显示名称：我的超棒助手
- 描述：帮助用户完成 XXX 功能
- 关键词：keyword1, keyword2
- 是否需要 MCP Server：是/否
```

### 步骤 2：我会生成完整骨架

包含以下文件：

```
my-awesome-power/
├── POWER.md              # Power 配置
├── README.md             # 项目说明
├── LICENSE               # MIT 许可证
├── package.json          # 版本管理
├── .versionrc.json       # CHANGELOG 配置
├── .gitignore            # Git 忽略规则
├── CHANGELOG.md          # 变更日志
├── mcp.json              # MCP 配置
├── .github/
│   └── workflows/
│       └── release.yml   # 自动发布工作流
└── steering/
    └── getting-started.md
```

### 步骤 3：初始化并发布

```bash
cd my-awesome-power
pnpm install
# 在 GitHub 创建仓库后
git remote add origin https://github.com/your-org/my-awesome-power.git
git push -u origin dev
git push -u origin main
pnpm release:first
```

## Steering 文件映射

| 任务场景 | Steering 文件 | 说明 |
| -------- | ------------- | ---- |
| 创建 Power | `steering/template-generator.md` | 完整骨架生成指南 |
| Power 结构 | `steering/power-structure.md` | 目录结构规范 |
| POWER.md 配置 | `steering/power-config.md` | 配置文件指南 |
| 提交规范 | `steering/commit-convention.md` | Conventional Commits |
| 版本发布 | `steering/version-release.md` | 发布工作流 |

## 生成的工作流

**分支结构：**
- `dev` - 开发分支（完整开发环境）
- `main` - 发布分支（只有 Power 必需文件）

**发布流程：**
```bash
pnpm release        # 一键发布！
```

自动执行：
1. 更新版本号和 CHANGELOG
2. 创建 Git tag
3. 推送到 dev 分支
4. GitHub Actions 自动同步到 main 分支
5. 创建 GitHub Release

## 常见问题

### Q: 如何选择版本类型？

```bash
pnpm release        # 自动判断（推荐）
pnpm release:patch  # Bug 修复 0.1.0 → 0.1.1
pnpm release:minor  # 新功能 0.1.0 → 0.2.0
pnpm release:major  # 破坏性变更 0.1.0 → 1.0.0
```

### Q: 用户如何安装我的 Power？

用户在 Kiro Powers 面板添加你的 GitHub 仓库地址即可。
