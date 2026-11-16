# 我的技术文档

使用 MkDocs Material 搭建的四页静态文档站，通过 GitHub Actions 自动构建并部署到 GitHub Pages。

- 🌐 网站地址：https://fugory.github.io/my-docs/
- 📄 个人实验报告：[report/README.md](report/README.md)
- 📦 源码仓库：https://github.com/fugory/my-docs

## 项目简介

本项目验证一条完整的发布链路：**推送 Markdown → CI 自动构建 → 自动发布 → 网页更新**。

- `docs/` 存放 Markdown 源文件，是唯一的内容来源。
- `site/` 是构建产物，由 CI 生成，不提交进仓库（见 `.gitignore`）。
- `.github/workflows/deploy.yml` 定义构建与部署流程。
- `report/` 存放实验报告与过程截图。

## 本地预览

```bash
python -m venv .venv
source .venv/bin/activate        # Windows Git Bash
# Windows PowerShell: .\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt

python -m mkdocs serve           # 本地预览 http://127.0.0.1:8000/
python -m mkdocs build --strict  # 严格构建，推送前必做
```

## 目录结构

```
my-docs/
├── .github/workflows/deploy.yml
├── docs/
│   ├── index.md
│   ├── about.md
│   ├── guide.md
│   └── api.md
├── report/
│   ├── README.md
│   └── images/
├── mkdocs.yml
├── requirements.txt
└── .gitignore
```
