# 使用指南

## 日常流程

1. 修改 `docs` 目录中的 Markdown 文件。
2. 在本地预览并检查页面及链接。
3. 提交修改并推送到 `main` 分支。
4. 在 Actions 页面查看构建与部署状态。
5. 打开网站检查内容是否更新。

## 常用命令

本地安装依赖（建议在虚拟环境中）：

```bash
python -m venv .venv
source .venv/bin/activate      # Windows Git Bash
python -m pip install -r requirements.txt
```

构建与预览：

- `python -m mkdocs serve`：本地预览，默认地址 `http://127.0.0.1:8000/`，改文件会自动热重载。
- `python -m mkdocs build --strict`：构建网站并严格检查警告，警告即报错。

两者区别值得注意：`serve` 只告诉你"页面能打开"，`build --strict` 才会把断链、配置错误拦下来。**推送前一定要跑一次 `--strict`**，因为 CI 里跑的就是它。

## 每个动作对应什么结果

| 你的动作 | 触发的反应 | 等待时间 |
| --- | --- | --- |
| 改 `docs/*.md` 并推送 | 自动构建 + 自动部署 | 约 30–60 秒 |
| 改 `mkdocs.yml` 或 `requirements.txt` | 自动构建 + 自动部署 | 约 1–2 分钟 |
| 只改 `README.md` 或 `report/` | 不触发任何工作流 | — |
| 在 Actions 页面点 Run workflow | 手动构建 + 部署 | 同上 |

## 出问题先看哪里

按这个顺序查，通常一跳就能定位：

1. **Actions 里是红的哪一步？** 展开看日志最后 20 行。
2. 卡在 `Build documentation` → 本地跑 `--strict` 复现，报错信息是一样的。
3. 卡在 `Deploy to GitHub Pages` → 先看 Settings → Pages 的 Source 是不是 `GitHub Actions`。
4. 全绿但网站没变 → 等 20 秒再无痕窗口刷新，多半是 CDN 缓存。

## 一点实践体会

这份指南里最有价值的一行不是命令，是"**推送前先跑 `--strict`**"。

原因是 CI 的失败反馈回路很长：推送 → 等排队 → 等构建 → 看红字 → 改 → 再推，一轮三五分钟。而在本地跑同一条命令只要几秒。把检查放在本地，等于把长回路换成短回路 —— 这个思路比记任何命令都有用。
