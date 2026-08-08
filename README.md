# 工作台集（my-dashboards）

多个个人工作台的统一仓库。打开 GitHub Pages 即用，数据存私有仓库，git 版本化。

## 工作台列表

| 工作台 | 地址 | 说明 |
|---|---|---|
| 科研工作台 | [`/research/`](./research/index.html) | 论文进度 / 文献 / 灵感 / 日志 |

## 架构

- **壳仓库（本仓库，public）**：工作台网页，无敏感数据
- **数据仓库 `my-dashboards-data`（private）**：各工作台数据 JSON，工作台通过 GitHub API 读写

## 新增工作台

1. 复制 `research/` 目录为 `finance/`（或新名字）
2. 在数据仓库创建对应数据文件路径
3. 修改页面内数据路径配置
4. 推送 → Pages 自动更新

## 本地预览

直接打开 `research/index.html`，或起任意静态服务器。
