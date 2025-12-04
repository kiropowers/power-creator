# Power 结构规范

本文件指导如何创建标准的 Kiro Power 骨架工程。

## Power 类型

### 类型 1：纯 Steering Power

只提供文档和指导，不需要 MCP 工具：

```
my-power/
├── POWER.md              # [必需] Power 配置和文档
├── steering/             # [必需] Steering 指导文件
│   └── getting-started.md
├── README.md             # [推荐] 项目说明
└── LICENSE               # [推荐] 许可证
```

适用场景：代码规范、最佳实践、工作流指导等。

### 类型 2：带 MCP Server 的 Power

提供工具调用能力：

```
my-power/
├── POWER.md              # [必需] Power 配置和文档
├── mcp.json              # [必需] MCP Server 配置
├── steering/             # [推荐] Steering 指导文件
│   └── getting-started.md
├── README.md             # [推荐] 项目说明
└── LICENSE               # [推荐] 许可证
```

适用场景：数据库操作、API 调用、文件处理等需要工具的场景。

## 完整目录结构（带版本管理）

```
my-power/
├── POWER.md              # [必需] Power 配置和文档
├── mcp.json              # [可选] MCP Server 配置
├── README.md             # [推荐] 项目说明
├── LICENSE               # [推荐] 许可证
├── package.json          # [推荐] 版本管理
├── .versionrc.json       # [推荐] CHANGELOG 配置
├── .gitignore            # [推荐] Git 忽略规则
├── CHANGELOG.md          # [推荐] 变更日志
└── steering/             # [推荐] Steering 指导文件
    ├── getting-started.md
    └── ...
```

## 必需文件

### POWER.md

Power 的核心配置文件，包含：

```yaml
---
name: "power-name"           # Power 标识符（小写，连字符分隔）
displayName: "显示名称"       # 用户看到的名称
description: "功能描述"       # 简短描述
keywords:                    # 激活关键词
  - "关键词1"
  - "keyword2"
---
```

### mcp.json（如需 MCP Server）

```json
{
  "mcpServers": {
    "server-name": {
      "command": "uvx",
      "args": ["package-name@latest"],
      "env": {
        "ENV_VAR": "value"
      }
    }
  }
}
```

## POWER.md 模板

```markdown
---
name: "{{power-name}}"
displayName: "{{显示名称}}"
description: "{{功能描述}}"
keywords:
  - "{{关键词1}}"
  - "{{关键词2}}"
---

# {{显示名称}}

{{详细功能描述}}

## 何时激活

当用户讨论以下内容时激活此 Power：

- {{场景1}}
- {{场景2}}

## Onboarding

### 步骤 1：{{步骤标题}}

{{步骤说明}}

## Steering 文件映射

| 任务场景 | Steering 文件 | 说明 |
| -------- | ------------- | ---- |
| {{场景}} | `steering/{{file}}.md` | {{说明}} |

## 快速命令

\`\`\`bash
# {{命令说明}}
{{命令}}
\`\`\`

## 常见问题

### Q: {{问题}}？

{{答案}}
```

## Steering 文件规范

### 文件命名

- 使用小写字母和连字符
- 描述性命名：`getting-started.md`, `api-reference.md`

### 文件结构

```markdown
# 标题

简短描述本文件的用途。

## 章节 1

内容...

## 章节 2

内容...
```

### 条件加载

在 steering 文件头部添加 front-matter：

```yaml
---
inclusion: fileMatch
fileMatchPattern: "*.py"
---
```

## 创建步骤

1. 确定 Power 名称和功能
2. 创建目录结构
3. 编写 POWER.md
4. 添加 steering 文件
5. 配置版本管理
6. 初始化 Git 仓库
7. 发布到 GitHub
