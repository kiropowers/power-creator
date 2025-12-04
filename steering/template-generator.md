# Power 骨架生成指南

本文件指导如何为用户生成完整的 Power 开发骨架工程。

## 生成流程

当用户请求创建新 Power 时，按以下步骤执行：

### 1. 收集信息

从用户请求中提取：

- **name**: Power 标识符（小写，连字符分隔）
- **displayName**: 显示名称
- **description**: 功能描述
- **keywords**: 关键词列表
- **needsMcp**: 是否需要 MCP Server

### 2. 创建目录结构

```bash
mkdir {{power-name}}
mkdir {{power-name}}/steering
mkdir {{power-name}}/.github
mkdir {{power-name}}/.github/workflows
```

### 3. 生成文件清单

**开发环境文件（dev 分支）：**
1. `POWER.md` - Power 配置
2. `README.md` - 项目说明
3. `LICENSE` - MIT 许可证
4. `package.json` - 版本管理（含自动推送）
5. `.versionrc.json` - CHANGELOG 配置
6. `.gitignore` - Git 忽略规则
7. `CHANGELOG.md` - 变更日志
8. `mcp.json` - MCP 配置（如需要）
9. `.github/workflows/release.yml` - 自动发布工作流
10. `steering/getting-started.md` - 入门指南

**发布文件（main 分支，自动同步）：**
- `POWER.md`
- `README.md`
- `LICENSE`
- `mcp.json`（如有）
- `steering/`

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
    "release": "standard-version && git push --follow-tags origin dev",
    "release:patch": "standard-version --release-as patch && git push --follow-tags origin dev",
    "release:minor": "standard-version --release-as minor && git push --follow-tags origin dev",
    "release:major": "standard-version --release-as major && git push --follow-tags origin dev",
    "release:first": "standard-version --first-release && git push --follow-tags origin dev"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/{{org}}/{{name}}.git"
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

### .github/workflows/release.yml

```yaml
name: Release to Main

on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout dev branch
        uses: actions/checkout@v4
        with:
          ref: dev
          fetch-depth: 0

      - name: Configure Git
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"

      - name: Get version from tag
        id: version
        run: echo "version=${GITHUB_REF#refs/tags/v}" >> $GITHUB_OUTPUT

      - name: Checkout main branch
        run: |
          git checkout main
          git pull origin main

      - name: Copy release files to main
        run: |
          git checkout dev -- POWER.md README.md LICENSE steering/
          # 如果有 mcp.json 也复制
          git checkout dev -- mcp.json 2>/dev/null || true
          
      - name: Commit and push to main
        run: |
          git add .
          git commit -m "release: v${{ steps.version.outputs.version }}" || echo "No changes to commit"
          git tag -f v${{ steps.version.outputs.version }}
          git push origin main
          git push -f origin v${{ steps.version.outputs.version }}

      - name: Create GitHub Release
        uses: softprops/action-gh-release@v1
        with:
          tag_name: v${{ steps.version.outputs.version }}
          name: Release v${{ steps.version.outputs.version }}
          generate_release_notes: true
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### mcp.json（如需 MCP Server）

```json
{
  "mcpServers": {
    "{{server-name}}": {
      "command": "uvx",
      "args": ["{{package-name}}@latest"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      }
    }
  }
}
```

如果是纯 Steering Power，使用空配置：

```json
{
  "mcpServers": {}
}
```

### README.md

```markdown
# {{displayName}}

{{description}}

## 安装

在 Kiro 中通过 Powers 面板添加此仓库。

## 开发

### 环境准备

\`\`\`bash
# 克隆仓库
git clone https://github.com/{{org}}/{{name}}.git
cd {{name}}

# 切换到开发分支
git checkout dev

# 安装依赖
pnpm install
\`\`\`

### 发布新版本

\`\`\`bash
pnpm release        # 自动判断版本号
pnpm release:patch  # 补丁版本 0.1.0 → 0.1.1
pnpm release:minor  # 次版本 0.1.0 → 0.2.0
pnpm release:major  # 主版本 0.1.0 → 1.0.0
\`\`\`

发布命令会自动：
1. 更新版本号
2. 生成 CHANGELOG
3. 创建 Git tag
4. 推送到 dev 分支
5. 触发 GitHub Actions 同步到 main 分支

## 分支说明

- `dev` - 开发分支，包含完整开发环境
- `main` - 发布分支，只包含 Power 必需文件

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

### CHANGELOG.md

```markdown
# Changelog

All notable changes to this project will be documented in this file.
```

### LICENSE

```
MIT License

Copyright (c) {{year}}

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 生成后初始化 Git

生成所有文件后，执行以下命令初始化仓库：

```bash
cd {{power-name}}

# 初始化 Git
git init

# 创建 dev 分支并提交
git checkout -b dev
git add .
git commit -m "feat: initial release"

# 创建空的 main 分支
git checkout --orphan main
git rm -rf .
git commit --allow-empty -m "chore: initialize main branch"

# 回到 dev 分支
git checkout dev

# 关联远程仓库（用户需要先在 GitHub 创建仓库）
echo ""
echo "请在 GitHub 创建仓库后执行："
echo "git remote add origin https://github.com/{{org}}/{{name}}.git"
echo "git push -u origin dev"
echo "git push -u origin main"
echo ""
echo "然后执行首次发布："
echo "pnpm install"
echo "pnpm release:first"
```

## 生成后提示用户

```
✅ Power 骨架已创建完成！

📁 目录结构：
{{power-name}}/
├── POWER.md
├── README.md
├── LICENSE
├── package.json
├── .versionrc.json
├── .gitignore
├── CHANGELOG.md
├── mcp.json
├── .github/
│   └── workflows/
│       └── release.yml
└── steering/
    └── getting-started.md

📋 下一步：
1. cd {{power-name}}
2. 在 GitHub 创建仓库 {{org}}/{{name}}
3. git remote add origin https://github.com/{{org}}/{{name}}.git
4. git push -u origin dev
5. git push -u origin main
6. pnpm install
7. pnpm release:first

🚀 日常开发流程：
- 在 dev 分支开发
- 提交代码：git commit -m "feat: xxx"
- 发布版本：pnpm release
```
