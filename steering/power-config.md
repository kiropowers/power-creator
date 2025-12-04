# POWER.md 配置指南

本文件详细说明 POWER.md 的配置选项和最佳实践。

## Front Matter 配置

### 必填字段

```yaml
---
name: "my-power"              # Power 唯一标识符
displayName: "我的 Power"      # 显示名称
description: "功能描述"        # 简短描述（一句话）
keywords:                     # 激活关键词列表
  - "关键词"
---
```

### 字段说明

| 字段 | 类型 | 必填 | 说明 |
| ---- | ---- | ---- | ---- |
| name | string | ✅ | 唯一标识符，小写，连字符分隔 |
| displayName | string | ✅ | 用户界面显示的名称 |
| description | string | ✅ | 简短功能描述 |
| keywords | string[] | ✅ | 触发激活的关键词 |

## 关键词设计

### 原则

1. **覆盖面广**：包含中英文关键词
2. **精准匹配**：避免过于通用的词
3. **场景导向**：基于用户使用场景

### 示例

```yaml
keywords:
  # 功能相关
  - "版本"
  - "version"
  - "changelog"
  
  # 动作相关
  - "发布"
  - "release"
  
  # 技术相关
  - "semver"
  - "conventional"
```

## 文档结构

### 推荐章节

```markdown
# Power 名称

简介段落

## 何时激活

列出激活场景

## Onboarding

用户首次使用的引导步骤

## Steering 文件映射

任务与 steering 文件的对应关系

## 快速命令

常用命令速查

## 常见问题

FAQ
```

## 何时激活

描述 Power 应该被激活的场景：

```markdown
## 何时激活

当用户讨论以下内容时激活此 Power：

- 创建新项目
- 配置开发环境
- 部署应用
```

## Onboarding 设计

### 步骤化引导

```markdown
## Onboarding

### 步骤 1：检查环境

确保已安装必要工具：

\`\`\`bash
node --version
\`\`\`

### 步骤 2：安装依赖

\`\`\`bash
pnpm install
\`\`\`

### 步骤 3：配置项目

创建配置文件...
```

### 最佳实践

1. 步骤清晰，每步只做一件事
2. 提供可执行的命令
3. 说明预期结果
4. 处理常见错误

## Steering 文件映射

建立任务与指导文件的对应关系：

```markdown
## Steering 文件映射

| 任务场景 | Steering 文件 | 说明 |
| -------- | ------------- | ---- |
| 初始配置 | `steering/setup.md` | 项目初始化 |
| 日常开发 | `steering/development.md` | 开发工作流 |
| 发布部署 | `steering/deployment.md` | 部署指南 |
```

## 快速命令

提供常用命令的速查表：

```markdown
## 快速命令

\`\`\`bash
# 开发
pnpm dev

# 构建
pnpm build

# 测试
pnpm test

# 发布
pnpm release
\`\`\`
```

## 常见问题

FAQ 格式：

```markdown
## 常见问题

### Q: 如何解决 XXX 问题？

答案...

### Q: 为什么会出现 YYY？

答案...
```
