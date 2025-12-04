# 版本发布工作流

本文件指导如何正确发布新版本。

## 版本号规则（SemVer）

```
MAJOR.MINOR.PATCH
  │     │     │
  │     │     └── Bug 修复、小改动
  │     └──────── 新功能（向后兼容）
  └────────────── 破坏性变更
```

### 版本号自动计算

| 提交类型        | 版本变化 | 示例            |
| --------------- | -------- | --------------- |
| fix             | PATCH    | 0.1.0 → 0.1.1   |
| feat            | MINOR    | 0.1.0 → 0.2.0   |
| BREAKING CHANGE | MAJOR    | 0.1.0 → 1.0.0   |

## 发布命令

### 自动发布（推荐）

```bash
# 根据提交类型自动判断版本号
pnpm release
```

### 指定版本类型

```bash
pnpm release:patch   # 0.1.0 → 0.1.1
pnpm release:minor   # 0.1.0 → 0.2.0
pnpm release:major   # 0.1.0 → 1.0.0
```

### 首次发布

```bash
pnpm release:first
```

### 预览模式

```bash
pnpm release -- --dry-run
```

## 发布前检查清单

- [ ] 所有功能已测试
- [ ] 文档已更新
- [ ] POWER.md 配置正确
- [ ] steering 文件完整

## 发布流程

```bash
# 1. 确保在主分支
git checkout main
git pull origin main

# 2. 预览发布
pnpm release -- --dry-run

# 3. 确认无误后发布
pnpm release

# 4. 推送到远程
git push --follow-tags origin main
```

## standard-version 自动执行的操作

1. 分析提交历史
2. 计算新版本号
3. 更新 package.json 版本
4. 生成/更新 CHANGELOG.md
5. 创建 Git commit
6. 创建 Git tag

## 特殊场景

### 预发布版本

```bash
# Alpha 版本
pnpm release -- --prerelease alpha

# Beta 版本
pnpm release -- --prerelease beta
```

### 指定版本号

```bash
pnpm release -- --release-as 1.0.0
```

## 发布后操作

```bash
# 推送代码和标签
git push --follow-tags origin main
```

## 回滚版本

```bash
# 删除本地 tag
git tag -d v0.2.0

# 删除远程 tag
git push origin :refs/tags/v0.2.0

# 回退 commit
git reset --hard HEAD~1
```
