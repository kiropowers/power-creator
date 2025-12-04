# Power Creator

快速创建 Kiro Power 骨架工程的助手，自带版本管理和发布功能。

## 功能

- 🚀 一键创建 Power 骨架工程
- 📦 自带版本管理（standard-version）
- 📝 自动生成 CHANGELOG
- 📋 Conventional Commits 规范
- 🎯 完整的 Steering 指导文件

## 安装

在 Kiro 中通过 Powers 面板添加此仓库。

## 使用

激活 Power 后，告诉 Kiro 你想创建的 Power：

```
创建一个名为 "my-power" 的 Power，用于 XXX 功能
```

## 生成的骨架结构

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

## 版本管理

```bash
# 安装依赖
pnpm install

# 发布版本
pnpm release           # 自动判断版本号
pnpm release:patch     # 补丁版本
pnpm release:minor     # 次版本
pnpm release:major     # 主版本
```

## License

MIT
