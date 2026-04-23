# task-summary_cicd-cli-enhance_20260423-1218.md

## Objective
为 cicd-init CLI 工具添加 Docker 支持、服务器一键部署脚本、GitHub 仓库，修复 YAML 缩进 bug。

## Changes Made
1. **Dockerfile** - 基于 python:3.12-alpine，内置 git，ENTRYPOINT=cicd-init
2. **scripts/deploy-server.sh** - 服务器一键部署，支持 3 种方式：pipx（推荐）/ venv / Docker，自动检测系统包管理器（apt/yum/apk）
3. **Makefile** - install / dev / docker / docker-run / test / clean
4. **.gitignore** - Python 标准忽略规则
5. **README.md** - 新增 Docker 使用、服务器部署、开发命令章节
6. **templates.py** - 修复 GitHub Actions YAML 缩进 bug（`- run:` 从 6 空格修正为 4 空格），重构 `_gha_setup_steps()` 为独立函数

## GitHub Repository
- URL: https://github.com/webkubor/cicd-init
- Account: webkubor
- Default branch: main
- Visibility: public

## Server Deployment
三种方式，一行命令：
```bash
# pipx（推荐）
curl -sL https://raw.githubusercontent.com/webkubor/cicd-init/main/scripts/deploy-server.sh | bash -s -- --method=pipx

# Docker
curl -sL https://raw.githubusercontent.com/webkubor/cicd-init/main/scripts/deploy-server.sh | bash -s -- --method=docker

# venv（安装到 /opt/cicd-init）
curl -sL https://raw.githubusercontent.com/webkubor/cicd-init/main/scripts/deploy-server.sh | bash -s -- --method=venv
```

## Verified
- ✅ GitHub Actions YAML 缩进正确（- run: 与 - uses: 同级）
- ✅ pip install -e . 成功
- ✅ dry-run 输出格式正确
- ✅ git push 到 github.com/webkubor/cicd-init 成功
