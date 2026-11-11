# 部署说明

本仓库是 [xiaoyang111222/cn-math-taxonomy](https://github.com/xiaoyang111222/cn-math-taxonomy) 的静态站点部署镜像，用于通过 GitHub Pages 在公网访问「中小学·高中知识图谱」。

- **授权**：沿用上游 [LICENSE](./LICENSE)（CC BY-NC 4.0），仅供个人学习、教学、研究等非商业用途；署名与许可文件保持原样。
- **内容**：知识点先修关系与题库为上游 AI 生成初稿，正式教学或诊断前请由一线教师审核。
- **相对上游的改动**：
  1. `assets/stats-config.js` 的 `endpoint` 置空，避免把本站访客数据通过 `sendBeacon` 上报给上游第三方采集 Worker。恢复方式见该文件注释。
  2. 新增 `.github/workflows/pages.yml`：推送到 `main` 后自动把静态站点发布到 GitHub Pages。
  3. 新增 `.nojekyll`：关闭 Jekyll 处理，保证静态文件原样发布。
- **站点结构**：纯静态，无构建、无后端、无数据库。数据全部来自 `data/*.json`，孩子档案与诊断记录保存在浏览器 localStorage。
- **本地预览**：不能用 `file://` 直接打开（fetch 读 JSON 会跨域），请用 `python -m http.server 8080` 后访问 `http://127.0.0.1:8080/`。
- **更新站点**：向 `main` 推送提交即可，Pages 工作流会自动重新部署。
