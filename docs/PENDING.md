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
| BATCH-02 | 六家官网/SDK 本地预备材料 | 已撤销 | 已从仓库与 Pages 范围移除，站点只展示中文文档 |
| BATCH-02b | PlacementSpec（`docs/design/04`） | 已屏蔽 | gitignore；不进仓库展示、不进 Pages |
| BATCH-03 | 官网英文文档 → 中文整合站（GH Pages） | 完成 | 见线上站点 |

## 待办（后续）

- [ ] 各 `portal-map` 中仍标「待写」的细目（如 MAX Flutter/RN、LevelPlay APIs/Account、AdSense 报表等）
- [x] 创建 GitHub 仓库、推送、打开 Pages
- [x] 移除 `materials/sdk`，Pages / 仓库仅保留文档站

## 已完成

- [x] 台账文档 `docs/design/01`、`02`、`03`
- [x] 中文站 `site/` + Pages 部署
- [x] 去掉 SDK 二进制；反编译衍生笔记不进 git / 不在站上展示
