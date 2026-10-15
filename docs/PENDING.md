# PENDING

> 编写模型: Composer (Cursor Agent) · 2026-10-15

出海广告接入指北 · 进行中事项索引。

## 进行中

| ID | 事项 | 状态 | 说明 |
|----|------|------|------|
| BATCH-03a | 中文文档站骨架（Docsify + 版权 + 选题对照） | 完成 | `site/`、`docs/design/03` |
| BATCH-03b | 六入口起步中文页 + 总览/聚合 | 完成 | `site/platforms/*`、`mediation/` |
| BATCH-03c | 广告格式深页 / 结算 / 隐私 / ads.txt | 完成 | 5 路深页已落盘；侧栏/catalog 已人工合并收口 |
| BATCH-03d | 推 GitHub + 开启 Pages 核对线上 | 完成 | https://kongliuli.github.io/haiwai-ads-guide/ · 仓库 kongliuli/haiwai-ads-guide |
| BATCH-04 | 对齐各厂商官方文档平台并补中文栏目 | 完成 | 五家 `portal-map` + 栏目深页；侧栏完整；地图内少数项仍标待写 |

## 台账速览

| ID | 事项 | 状态 |
|----|------|------|
| BATCH-01 | 主流平台总览 + 聚合策略（台账文档） | 完成 |
| BATCH-02 | 六家官网/SDK 本地预备材料 | 完成 |
| BATCH-02b | REA 拆 SDK → PlacementSpec（`docs/design/04`） | 完成 |
| BATCH-03 | 官网英文文档 → 中文整合站（GH Pages） | 03a/b 完成；03c/d 待办 |

## 待办（后续）

- [ ] 各 `portal-map` 中仍标「待写」的细目（如 MAX Flutter/RN、LevelPlay APIs/Account、AdSense 报表等）
- [x] 创建 GitHub 仓库、推送、打开 Pages，回填线上 URL 到 README
- [ ] Meta AN iOS 官方手动 ZIP 若放出再补 `materials/sdk`

## 已完成

- [x] 第一批台账文档 `docs/design/01`、`02`
- [x] SDK 预备 `materials/sdk/` + PlacementSpec `docs/design/04`
- [x] REA 拆解分发/呈现/Bridge，归纳广告位元数据
- [x] 中文站骨架与起步内容 `site/`
- [x] Pages 部署工作流 `.github/workflows/deploy-pages.yml`
