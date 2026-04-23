# task-summary_cicd-beginner-ux_20260423-1227

## Objective
让 cicd-init 对小白用户友好：一行命令安装，一行命令使用，配置极简。

## Changes

### 1. install.sh — 一键安装脚本
- `curl -sL https://raw.githubusercontent.com/webkubor/cicd-init/main/install.sh | bash`
- 自动检测/安装 Python 3.8+、pip
- 支持 macOS (brew) / Ubuntu (apt) / CentOS (yum) / Alpine (apk)
- 自动处理 PATH（~/.local/bin）
- 安装完成后提示下一步操作

### 2. --simple 极简模式
- `cicd-init init --simple` 只生成 install → build 两步
- 适合新手：不强制 lint/test/typecheck，只关心"能不能构建成功"
- Full 模式不变，团队项目继续用完整检查链

### 3. README 重写
- 60 秒上手放在最前面
- 新手视角："不懂 CI/CD？没关系，跑一下就行"
- 两种模式清晰对比

### 4. 代码改动
- cli.py: 新增 --simple flag
- generator.py: 传递 simple 参数到模板
- templates.py: simple=True 时生成精简 YAML（GitLab: 2 stages, GitHub: 1 job）

## Verified
- ✅ full mode: typecheck + lint + test + build (不变)
- ✅ simple mode: 只有 build job (极简)
- ✅ install.sh 可执行权限正确
- ✅ push 到 github.com/webkubor/cicd-init 成功
