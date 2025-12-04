# Power Creator

[English](README.md) | [中文](README.zh-CN.md)

A Kiro Power for scaffolding new Power projects with complete development environment and automated release workflow.

## Features

- One-click Power skeleton generation
- dev/main dual-branch workflow
- Automated versioning (standard-version)
- Auto-generated CHANGELOG
- GitHub Actions auto-release
- Conventional Commits support

## Installation

Add this repository via Kiro Powers panel.

## Usage

After activating the Power, tell Kiro what Power you want to create:

```
Create a Power:
- Name: my-power
- Display Name: My Awesome Power
- Description: Helps users do XXX
- Keywords: keyword1, keyword2
```

## Generated Skeleton Structure

```
my-power/
├── POWER.md              # Power configuration
├── README.md             # Project description
├── LICENSE               # MIT License
├── package.json          # Version management
├── .versionrc.json       # CHANGELOG config
├── .gitignore            # Git ignore rules
├── CHANGELOG.md          # Change log
├── mcp.json              # MCP configuration
├── .github/
│   └── workflows/
│       └── release.yml   # Auto release
└── steering/
    └── getting-started.md
```

## Development

```bash
# Clone repository
git clone https://github.com/kiropowers/power-creator.git
cd power-creator
git checkout dev
pnpm install
```

## Release

```bash
pnpm release        # Auto determine version
pnpm release:patch  # Patch version
pnpm release:minor  # Minor version
pnpm release:major  # Major version
```

## Branch Description

- `dev` - Development branch with full dev environment
- `main` - Release branch with only Power essential files

## License

MIT
