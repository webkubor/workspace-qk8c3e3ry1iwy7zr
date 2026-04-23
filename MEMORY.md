# MEMORY.md

## 用户信息
- GitHub: webkubor
- 机器: 王恩博的MacBook Pro (macOS Darwin 24.6.0, ARM64)
- Python: 3.14.3
- Claude Code 环境: ~/Library/Application Support/QClaw/

## GitHub 仓库
- **cicd-init**: https://github.com/webkubor/cicd-init — 前端项目 CI/CD 自动生成工具
- **workspace**: https://github.com/webkubor/workspace-qk8c3e3ry1iwy7zr — 本工作区同步仓库

## cicd-init 工具详情
- 功能：自动探测前端项目，生成 GitLab CI / GitHub Actions YAML
- 安装：`curl -sL https://raw.githubusercontent.com/webkubor/cicd-init/main/install.sh | bash`
- 模式：
  - `cicd-init init` → 完整模式（typecheck → lint → test → build）
  - `cicd-init init --simple` → 极简模式（install → build）
- 核心模块：detect.py, generator.py, templates.py
- 依赖：零外部依赖，纯 Python 标准库

## 偏好
- 喜欢极简：工具要小白能用，配置越少越好
- 风格：DevOps自动化师，CI/CD流水线专家

## 待办 / 项目
- cicd-init v0.1.0 已发布，GitHub Actions YAML 缩进 bug 已修复
- 用户希望 cicd-init 面向小白友好（极简模式已实现）
