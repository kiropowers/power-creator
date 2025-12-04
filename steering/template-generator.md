# Power 骨架生成指南

本文件指导如何为用户生成 Power 骨架工程。

## 生成流程

当用户请求创建新 Power 时，按以下步骤执行：

### 1. 收集信息

从用户请求中提取：

- **name**: Power 标识符（小写，连字符分隔）
- **displayName**: 显示名称
- **description**: 功能描述
- **keywords**: 关键词列表

### 2. 创建目录结构

```bash
mkdir {{power-name}}
mkdir {{power-name}}/steering
```

### 3. 生成文件

按以下顺序生成文件：

1. `POWER.md` - Power 配置
2. `package.json` - 版本管理
3. `.versionrc.json` - CHANGELOG 配置
4. `.gitignore` - Git 忽略规则
5. `LICENSE` - MIT 许可证
6. `CHANGELOG.md` - 变更日志
7. `README.md` - 项目说明
8. `steering/getting-started.md` - 入门指南

## 文件模板

### POWER.md

```markdown
---
name: "{{name}}"
displayName: "{{displayName}}"
description: "{{description}}"
keywords:
{{#each keywords}}
  - "{{this}}"
{{/each}}
---

# {{displayName}}

{{description}}

## 何时激活

当用户讨论以下内容时激活此 Power：

- {{使用场景1}}
- {{使用场景2}}

## Onboarding

### 步骤 1：开始使用

{{入门步骤}}

## Steering 文件映射

| 任务场景 | Steering 文件 | 说明 |
| -------- | ------------- | ---- |
| 入门 | `steering/getting-started.md` | 快速开始 |

## 常见问题

### Q: 如何使用此 Power？

激活后按照 Onboarding 步骤操作即可。
```

### package.json

```json
{
  "name": "{{name}}",
  "version": "0.1.0",
  "description": "{{description}}",
  "scripts": {
    "release": "standard-version",
    "release:patch": "standard-version --release-as patch",
    "release:minor": "standard-version --release-as minor",
    "release:major": "standard-version --release-as major",
    "release:first": "standard-version --first-release"
  },
  "devDependencies": {
    "standard-version": "^9.5.0"
  },
  "license": "MIT"
}
```

### .versionrc.json

```json
{
  "types": [
    { "type": "feat", "section": "✨ 新功能" },
    { "type": "fix", "section": "🐛 Bug 修复" },
    { "type": "docs", "section": "📚 文档更新" },
    { "type": "style", "section": "💄 代码格式" },
    { "type": "refactor", "section": "♻️ 代码重构" },
    { "type": "perf", "section": "⚡ 性能优化" },
    { "type": "test", "section": "✅ 测试" },
    { "type": "chore", "section": "🔧 构建/工具" },
    { "type": "ci", "section": "👷 CI 配置" }
  ]
}
```

### .gitignore

```
node_modules/
pnpm-lock.yaml
package-lock.json
yarn.lock
.DS_Store
*.log
```

### README.md

```markdown
# {{displayName}}

{{description}}

## 安装

在 Kiro 中通过 Powers 面板添加此仓库。

## 使用

激活 Power 后，按照 POWER.md 中的 Onboarding 步骤操作。

## 版本管理

\`\`\`bash
pnpm install
pnpm release
\`\`\`

## License

MIT
```

### steering/getting-started.md

```markdown
# 快速开始

本文件帮助你快速上手 {{displayName}}。

## 前置条件

- 已安装 Kiro
- 已激活此 Power

## 基本使用

{{根据 Power 功能编写具体使用说明}}

## 下一步

- 查看 POWER.md 了解更多功能
- 查看其他 steering 文件获取详细指导
```

## 生成后提示

生成完成后，提示用户：

1. 进入目录：`cd {{power-name}}`
2. 初始化 Git：`git init`
3. 安装依赖：`pnpm install`
4. 首次提交：`git add . && git commit -m "feat: initial release"`
5. 发布到 GitHub
