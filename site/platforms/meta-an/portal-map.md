# Meta Audience Network · 官方文档平台地图

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Audience Network 文档站](https://developers.facebook.com/docs/audience-network)（现多跳转至 [documentation/audience-network](https://developers.facebook.com/documentation/audience-network)）

官方站以 **App Bidding（应用竞价）** 为主线：个人开发者默认经聚合 Bidding，再对照平台设置 / 广告格式 / 政策。下表按当前侧栏栏目对齐本站进度。

状态：`已写` / `占位` / `待写`

## 栏目对照

| 官方栏目（中/英） | 官方入口 | 本站 | 状态 |
|-------------------|----------|------|------|
| 概览 / How to use this site | [how-to-use-this-site](https://developers.facebook.com/documentation/audience-network/how-to-use-this-site) | [index.md](index.md) | 已写 |
| 快速入门 / Quick start（Getting Started） | [quick-start](https://developers.facebook.com/documentation/audience-network/quick-start) | [index.md](index.md) | 已写 |
| 竞价集成 / Bidding Integration | [bidding-integration](https://developers.facebook.com/documentation/audience-network/bidding-integration) · [bidding/overview](https://developers.facebook.com/documentation/audience-network/bidding/overview) | [via-mediation.md](via-mediation.md) | 已写 |
| └ 合作伙伴中介（AdMob / MAX / LevelPlay 等） | [partner-mediation](https://developers.facebook.com/documentation/audience-network/bidding/partner-mediation) · [AdMob](https://developers.facebook.com/documentation/audience-network/bidding/partner-mediation/admob) · [MAX](https://developers.facebook.com/documentation/audience-network/bidding/partner-mediation/max) · [Unity LevelPlay](https://developers.facebook.com/documentation/audience-network/bidding/partner-mediation/ironsource) | [via-mediation.md](via-mediation.md) | 已写 |
| └ 竞价检查清单 / 指标 | [bidding-checklist](https://developers.facebook.com/documentation/audience-network/bidding/partner-mediation/bidding-checklist) · [metrics](https://developers.facebook.com/documentation/audience-network/bidding/metrics) | [via-mediation.md](via-mediation.md) · [reporting.md](reporting.md) | 已写 |
| 广告格式 / Ad formats | [ad-formats](https://developers.facebook.com/documentation/audience-network/ad-formats) | [ad-formats.md](ad-formats.md) | 已写 |
| 平台设置 · Android | [android](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/android) · [add-sdk](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/android/add-sdk) | [index.md](index.md)（摘要） | 已写 |
| 平台设置 · iOS | [ios](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/ios) · [add-sdk](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/ios/add-sdk) · [ATE](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/ios/advertising-tracking-enabled) · [SKAdNetwork](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/ios/SKAdNetwork) | [index.md](index.md)（摘要） | 已写 |
| 平台设置 · Unity | [unity](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/unity) | — | 待写 |
| 广告设置（按平台分格式实现） | [ad-setup](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup) | [ad-formats.md](ad-formats.md)（选型+规范；实现链官方） | 已写 |
| 测试设置 | [testing](https://developers.facebook.com/documentation/audience-network/setting-up/testing) | [via-mediation.md](via-mediation.md)#测试时注意 | 占位 |
| 最佳实践 / Guidelines | [best-practices](https://developers.facebook.com/documentation/audience-network/optimization/best-practices) · [layout](https://developers.facebook.com/documentation/audience-network/optimization/layout-best-practices) · [audio](https://developers.facebook.com/documentation/audience-network/optimization/audio-best-practices) | [guidelines.md](guidelines.md) | 已写 |
| └ 政策 / Policy | [an-policy](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/an-policy) · [dos-and-donts](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/an-policy/dos-and-donts) | [guidelines.md](guidelines.md) | 已写 |
| └ ads.txt / app-ads.txt | [authorized-sellers](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/authorized-sellers) · [app-ads](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/authorized-sellers-app-ads) | [ops/ads-txt](../../ops/ads-txt.md) · [guidelines](guidelines.md) | 已写 |
| └ COPPA / 数据处理 | [coppa](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/coppa) · [data-processing-options](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/data-processing-options) | [ops/privacy](../../ops/privacy.md) · [guidelines](guidelines.md) | 已写 |
| API · 报告 API v2（Reporting） | [report-api/guide-v2](https://developers.facebook.com/documentation/audience-network/optimization/report-api/guide-v2) · [apis 概览](https://developers.facebook.com/documentation/audience-network/optimization/apis) | [reporting.md](reporting.md) | 已写 |
| 帮助 | [support](https://developers.facebook.com/documentation/audience-network/support) · [Help Center](https://www.facebook.com/help/audiencenetwork) | — | 待写 |
| 收款 / Payments | 帮助中心收款 · 本站 [ops/payout](../../ops/payout.md) | [ops/payout](../../ops/payout.md) | 已写 |

## 推荐阅读顺序（个人开发者）

1. [概览](index.md) → 确认走聚合 Bidding  
2. [经聚合 Bidding 接入](via-mediation.md) → AdMob / MAX / LevelPlay  
3. [广告格式](ad-formats.md) → Placement 选型与展示规范  
4. [政策与展示规范](guidelines.md) → 上架前过一遍红线  
5. [报表与看数](reporting.md) → Monetization Manager / 报告 API  

返回：[各家官方文档平台对照](../../portals.md) · [选题对照 catalog](../../catalog.md)
