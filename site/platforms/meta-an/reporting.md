# Meta AN · 报表与看数

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[报告 API v2](https://developers.facebook.com/documentation/audience-network/optimization/report-api/guide-v2) · [APIs 概览](https://developers.facebook.com/documentation/audience-network/optimization/apis) · [竞价指标](https://developers.facebook.com/documentation/audience-network/bidding/metrics) · [变现管理工具 Monetization Manager](https://business.facebook.com/) · 帮助中心 [Audience Network](https://www.facebook.com/help/audiencenetwork)

官方有完整的 **Reporting API（报告 API）**；个人开发者日常看数优先用 **Monetization Manager** 控制台，再与主聚合后台的 Meta bidding 报表对照。

## 1. 控制台看数（推荐起步）

入口：[Monetization Manager / Business](https://business.facebook.com/)（登录后进入 Audience Network / 变现相关报表）。

建议核对：

| 看什么 | 说明 |
|--------|------|
| 预估收入 / eCPM | 冷启动与时区延迟常见；勿与聚合当日实时数强行逐小时对齐 |
| 请求、填充、展示、点击 | 无请求 → 先查聚合映射与 adapter；有请求无填充 → 库存/国家/账号状态 |
| 按 Property / Placement | 确认 Placement ID 是否打到正确广告位 |
| 按国家 / 平台 | Tier-1/2 与低填充市场差异大 |
| Delivery：standard vs bidding | Monetization Manager 下可按投放方式拆；个人默认应几乎全是 bidding |

同时打开**主聚合**报表（AdMob / MAX / LevelPlay），确认 Meta 作为 bidding 源有展示与收益。两边口径、时区、归因窗口不同，以排查「完全没数」为主，不要死磕小数差。

收款与 hold：见 [结算与收款](../../ops/payout.md)。无 payout 信息时常表现为长期无填充。

## 2. 报告 API v2（程序化）

官方文档：[报告 API](https://developers.facebook.com/documentation/audience-network/optimization/report-api/guide-v2)。

面向需要把 AN 数据拉进自有 BI / 对账脚本的场景。个人小体量通常**不必**先上 API。

### 前提条件（摘要）

- Meta 应用具备 Facebook 登录用例，并申请 **`read_audience_network_insights`**  
- 应用内实现 Facebook 登录，能成功调图谱 API 与该权限  
- 通过 Meta 应用审核  
- 使用**长期用户访问口令**（Monetization Manager / 商务管理平台里随手生成的用户口令**不可**用于此 API）

### 常用能力

- 端点形态：`/{ID}/adnetworkanalytics`（细节以官方参考为准）  
- 查询参数示例：`metrics`、`breakdowns`、`filters`、`aggregation_period`、`since` / `until`、`limit`、排序字段  
- 指标示例：预估收入、展示、广告请求、填充、点击、eCPM、预估 CTR，以及竞价相关（竞价响应率、响应数、胜出率等）  
- 细分常见：国家、平台、App、Property、Placement、Deal、Delivery Method（standard / bidding）等  

### 限制（摘要）

- 日期默认多按太平洋时区理解（除非文档另述）  
- 展示过少时部分收入指标可能不可用  
- 事件量未达下限时可能不报或近似  
- 小时级汇总通常只保留约 **72 小时**；日汇总可能更晚才稳定  
- 同步请求时间范围常见上限约 **8 天**；数据保留约 **540 天**  
- 大量数据建议**基于光标的分页**

鉴权与报错：用 [访问口令调试工具](https://developers.facebook.com/tools/debug/accesstoken/)；超时/过大结果时缩小 `limit` 或缩短 `since`–`until`。

## 3. 个人开发者排查顺序

1. Monetization Manager：Property / Placement 是否 Active，商店链接与授权是否报错  
2. 主聚合：Meta bidding 是否启用、ID 是否贴对、adapter 是否进包  
3. [app-ads.txt](../../ops/ads-txt.md) 与收款信息  
4. 仍需批量拉数 → 再上报告 API  

## 相关页

- [概览](index.md) · [经聚合 Bidding](via-mediation.md) · [政策](guidelines.md) · [栏目地图](portal-map.md)
