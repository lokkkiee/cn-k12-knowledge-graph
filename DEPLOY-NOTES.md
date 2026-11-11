# 部署说明

本仓库是 [xiaoyang111222/cn-math-taxonomy](https://github.com/xiaoyang111222/cn-math-taxonomy) 的静态站点源码镜像，用于通过 GitHub Pages 在公网访问「中小学·高中知识图谱」。

- **授权**：沿用上游 [LICENSE](./LICENSE)（CC BY-NC 4.0），仅供个人学习、教学、研究等非商业用途；署名与许可文件保持原样。
- **内容**：知识点先修关系与题库为上游 AI 生成初稿，正式教学或诊断前请由一线教师审核。
- **相对上游的改动**：
  1. `assets/stats-config.js` 的 `endpoint` 置空，避免把本站访客数据通过 `sendBeacon` 上报给上游第三方采集 Worker。恢复方式见该文件注释。
  2. 新增 `.nojekyll`：关闭 Jekyll 处理，保证静态文件原样发布。
- **实际发布方式（重要）**：线上站点**不是**由本仓库的 Pages 提供，而是托管在已启用 Pages 的用户级仓库 `lokkkiee/lokkkiee.github.io` 的 `cn-k12-knowledge-graph/` 子目录下。该仓库从 `main` 根目录发布，因此把站点文件放进同名子目录，`https://lokkkiee.github.io/cn-k12-knowledge-graph/` 即可直接生效，无需启用本仓库的 Pages、无需 GitHub Actions、无需构建命令。
  - 采用此方式的原因：启用 Pages 属于账号级操作，Actions 自带的 `GITHUB_TOKEN` 无权创建站点（`Resource not accessible by integration`）；本机网关又把 `api.github.com` 的请求 301 重写到网页端，无法通过 REST API 自动启用。用户级站点早已启用（`has_pages: true`），走子目录是零点击、不依赖设置页的最稳路径。
  - 本仓库保留完整源码与 Git 历史；`lokkkiee.github.io` 仓库中只**新增**了 `cn-k12-knowledge-graph/` 子目录和根目录的 `.nojekyll`，原有的待办清单 `index.html` 与 `README.md` 未改动。
- **站点地址**：`https://lokkkiee.github.io/cn-k12-knowledge-graph/`
- **站点结构**：纯静态，无构建、无后端、无数据库。数据全部来自 `data/*.json`，孩子档案与诊断记录保存在浏览器 localStorage。全站使用相对路径，manifest 的 `start_url` / `scope` 与 Service Worker 注册路径均为相对推导，可安全挂在子路径下（离线缓存、添加到主屏幕均正常）。
- **本地预览**：不能用 `file://` 直接打开（fetch 读 JSON 会跨域），请用 `python -m http.server 8080 --bind 127.0.0.1` 后访问 `http://127.0.0.1:8080/`。
- **更新站点**：把本仓库的 `index.html`、`sw.js`、`manifest.webmanifest`、`assets/`、`data/`、`children/`、`explore/`、`diagnose/` 等同步到 `lokkkiee/lokkkiee.github.io` 的 `cn-k12-knowledge-graph/` 子目录，然后向该仓库的 `main` 推送，Pages 自动重新发布。
- **撤销**：删除 `lokkkiee/lokkkiee.github.io` 中的 `cn-k12-knowledge-graph/` 子目录并推送即可，原有站点不受影响。
