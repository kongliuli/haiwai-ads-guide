# 出海广告接入指北

> 编写模型: Composer (Cursor Agent) · 2026-10-15

面向个人开发者的海外广告变现指南：**中文整合文档站**（拟挂 GitHub Pages）+ 平台选型台账 + SDK 本地预备材料。

## 中文文档站（给开发者读）

源码目录：[`site/`](site/)（Docsify，零构建）

| 本地预览 | 说明 |
|----------|------|
| `npx --yes serve site` | 用 HTTP 打开，勿 `file://` |
| 入口 | `site/README.md` → 侧栏平台与聚合 |

设计与版权策略：[docs/design/03-中文文档站.md](docs/design/03-中文文档站.md)

**上线**：推送到 GitHub 后，仓库 Settings → Pages → Build and deployment 选 **GitHub Actions**；工作流见 [`.github/workflows/deploy-pages.yml`](.github/workflows/deploy-pages.yml)。线上 URL 开通后回填此处。

> 本站是中文**整合重写**，不是各厂商官方文档镜像。每篇文首有对照原文链接。

## 仓库结构

```
site/                 # 对外中文文档站（GitHub Pages 发布根）
docs/                 # 项目台账（PENDING / design / requirements）
materials/sdk/        # 各平台 SDK 预备归档
.github/workflows/    # Pages 部署
```

## 台账入口

- [docs/PENDING.md](docs/PENDING.md) — 批次进度  
- [docs/design/01-主流平台总览.md](docs/design/01-主流平台总览.md)  
- [docs/design/02-聚合策略.md](docs/design/02-聚合策略.md)  
- [materials/sdk/README.md](materials/sdk/README.md) — 官网与 SDK 索引  
