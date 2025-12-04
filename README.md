# Power Creator

快速创建 Kiro Power 骨架工程的助手，包含完整的开发环境和自动化发布流程。

## 功能

- 🚀 一键创建 Power 骨架工程
- � dev本/main 双分支工作流
- � 自动化版本C管理（standard-version）
- �  自动生成 CHANGELOG
- 🤖 GitHub Actions 自动发布
- 📋 Conventional Commits 规范

## 安装

在 Kiro 中通过 Powers 面板添加此仓库。

## 使用

激活 Power 后，告诉 Kiro 你想创建的 Power：

```
创建一个 Power：
- 名称：my-power
- 显示名称：我的助手
- 描述：帮助用户完成 XXX
- 关键词：keyword1, keyword2
```

## 生成的骨架结构

```
my-power/
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
│       └── release.yml   # 自动发布
└── steering/
    └── getting-started.md
```

## 开发

```bash
# 克隆仓库
git clone https://github.com/kiropowers/power-creator.git
cd power-creator
git checkout dev
pnpm install
```

## 发布

```bash
pnpm release        # 自动判断版本号
pnpm release:patch  # 补丁版本
pnpm release:minor  # 次版本
pnpm release:major  # 主版本
```

## 分支说明

- `dev` - 开发分支，包含完整开发环境
- `main` - 发布分支，只包含 Power 必需文件

## License

MIT
