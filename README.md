# 工作台集（my-dashboards）

多个个人工作台的统一仓库。**浏览器打开网址即用**，数据存私有仓库，git 版本化，零本地安装。

## 🚀 工作台列表

| 工作台 | 地址 | 说明 |
|---|---|---|
| 科研工作台 | [`/research/`](./research/index.html) | 论文进度 / 文献 / 灵感 / 日志 |
| 投资工作台 | [`/finance/`](./finance/index.html) | 多市场投资台账（加密货币 / 持仓 / 期权 / 组合） |

## 快速开始（科研工作台）

打开：**https://70asunflower.github.io/my-dashboards/research/**

首次使用（一次性配置，约 2 分钟）：

1. 数据仓库已创建：`70asunflower/my-dashboards-data`（私有）
2. GitHub 生成 **fine-grained token**：
   - Settings → Developer settings → Personal access tokens → Fine-grained tokens
   - Repository access：只勾选 `my-dashboards-data`
   - Permissions → Contents：**Read and write**
3. 工作台点右上角「云同步」→ 填 Token + 仓库 `70asunflower/my-dashboards-data` → 保存
4. 点「立即推送到云端」完成首次备份（把本地数据推到云端）

之后：打开页面**自动加载云端数据**，任何改动**5 秒防抖自动推送**。

## 📊 架构

| 仓库 | 可见性 | 角色 |
|---|---|---|
| `my-dashboards`（本仓库） | public | 工作台网页（纯代码，无数据） |
| `my-dashboards-data` | **private** | 数据文件 `data/research.json`（API 读写） |

- 为什么双仓库：免费版私有仓库不能开 Pages → 代码放 public 壳（无数据），数据放 private 仓库（有 token 才能读写）
- 数据流：页面 → GitHub contents API → 私有仓库 JSON 文件 → git 自动版本化
- 断网兜底：localStorage 缓存，离线照常用，恢复后自动重试

## 📁 新增工作台

1. 复制 `research/` 目录为新名字（如 `finance/`）
2. 修改页面内数据路径（`data/research.json` → `data/finance.json`）
3. 数据仓库中按需建目录
4. 推送 → Pages 自动更新 → 打开 `https://70asunflower.github.io/my-dashboards/finance/`

> 说明：Token 存在浏览器 localStorage，同域名（70asunflower.github.io）所有工作台共享，配置一次即可。

## 🧰 本地开发

```bash
# 预览
python -m http.server 8080
# 打开 http://localhost:8080/research/
```

## 🛡 数据安全

- 数据只存在于：私有仓库 + 你的浏览器 localStorage + 你导出的备份
- public 壳仓库无任何个人数据
- Token 只存本浏览器，建议 fine-grained 仅授权数据仓库
- 重要数据请定期「导出 JSON 备份」

## 📈 万条数据性能

- 归档区懒渲染（点开才生成，20 条/页）
- 文献/灵感列表分页（50 条/页加载更多）
- 日志分页（60 条/页）
- 已完成条目自动归档，主列表只渲染"在管的"
