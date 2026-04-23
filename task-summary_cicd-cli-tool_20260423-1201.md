# task-summary_cicd-cli-tool_20260423-1201.md

## Objective
创建一个自定义 CLI 工具 `cicd-init`，在项目根目录执行即可自动探测前端技术栈并生成 GitLab CI / GitHub Actions 配置文件。

## Key Decisions
- **语言**: Python 3.8+，零外部依赖（纯标准库 argparse）
- **探测能力**: git remote → GitHub/GitLab（含自托管）、lock file → npm/yarn/pnpm、package.json → React/Vue/Angular/Next.js/Nuxt/Svelte、Node 版本 → .nvmrc/.node-version/engines、构建产物 → 按框架推断
- **包管理器支持**: npm (ci)、yarn (frozen-lockfile)、yarn-berry (immutable)、pnpm (frozen-lockfile + pnpm/action-setup)
- **流水线结构**: install → typecheck → lint → test → build（并行化，build 依赖前面所有 stage）

## File Structure
```
cicd-init/
├── pyproject.toml          # 项目配置，pip install -e .
├── README.md               # 完整使用文档
├── .venv/                  # Python 虚拟环境
└── cicd_init/
    ├── __init__.py         # 版本号 0.1.0
    ├── __main__.py         # python -m cicd_init 入口
    ├── cli.py              # argparse CLI（init / detect 命令）
    ├── detect.py           # 项目探测模块
    ├── generator.py        # 生成编排器
    └── templates.py        # YAML 模板生成器
```

## CLI Commands
```bash
cicd-init init                # 自动检测 git 远程仓库生成 CI 配置
cicd-init init -p gitlab      # 强制 GitLab
cicd-init init -p github      # 强制 GitHub
cicd-init init --all          # 同时生成两个平台
cicd-init init --dry-run      # 预览不写入
cicd-init init --node-version 18  # 覆盖 Node 版本
cicd-init detect              # 显示检测结果
```

## Verified
- ✅ 安装成功（pip install -e . in venv）
- ✅ detect 命令正确识别 React + Vite + npm + Node 20
- ✅ GitLab CI 生成正确的 .gitlab-ci.yml（stages, cache, needs, artifacts）
- ✅ GitHub Actions 生成正确的 ci.yml（concurrency, parallel jobs, cache, upload-artifact）
- ✅ --all 同时生成两个平台配置
