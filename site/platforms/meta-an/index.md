# Meta Audience Network · 概览与起步

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Audience Network 文档](https://developers.facebook.com/docs/audience-network) · [快速入门](https://developers.facebook.com/documentation/audience-network/quick-start) · [Android 加 SDK](https://developers.facebook.com/docs/audience-network/setting-up/platform-setup/android/add-sdk) · iOS [FBAudienceNetwork](https://github.com/facebook/FBAudienceNetwork)

## 这是什么

Meta Audience Network（AN）用 Meta 广告需求填充你的 App 广告位。在欧美及部分东南亚 **Tier-1 / Tier-2** 市场 eCPM 往往很有竞争力，但个人准入与合规要求高于 AdMob：通常要绑定 Facebook 账号、应用商店链接合规等。

官方文档站栏目地图（Getting Started、平台设置、广告格式、Bidding、政策、报表等）→ [portal-map.md](portal-map.md)

## 关键现实：请走聚合 Bidding

官方文档首页即以 **应用竞价（App Bidding）** 为主线。近年来 Meta 侧更强调通过 **Mediation Bidding** 接入（AdMob / MAX / LevelPlay 等），而不是长期单独直连 SDK 当唯一变现通道。个人开发者默认策略：

1. 选定主聚合层  
2. 在聚合后台启用 Meta adapter（Bidding）  
3. 完成 Meta 侧应用与广告位配置、签名与商店链接校验  

**实操清单与各聚合官方 adapter 入口** → [经聚合 Bidding 接入](via-mediation.md)

直连 SDK 仍可用于学习或特殊场景，但生产路径请以 Meta 与聚合平台当前要求为准。

## Android（直连摘要）

Maven：

```groovy
implementation("com.facebook.android:audience-network-sdk:6.22.0")
```

官方：[添加 SDK](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/android/add-sdk) · [初始化](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/android/initialize-sdk)

## iOS（直连摘要）

官方推荐 **Swift Package Manager**：

```text
https://github.com/facebook/FBAudienceNetwork
```

自 6.22.0 起强化 SPM；CocoaPods 逐渐弃用。GitHub Release 未必附带可直链的 xcframework zip——以 SPM / 文档为准。

注意：较新版本可能要求很高的 Xcode / 最低 iOS 版本（以 Release Note 为准）。另见 [ATE](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/ios/advertising-tracking-enabled) · [SKAdNetwork](https://developers.facebook.com/documentation/audience-network/setting-up/platform-setup/ios/SKAdNetwork)。

## 本站分篇

| 主题 | 页面 |
|------|------|
| 官方栏目地图 | [portal-map.md](portal-map.md) |
| 经聚合 Bidding | [via-mediation.md](via-mediation.md) |
| 广告格式 | [ad-formats.md](ad-formats.md) |
| 政策 / 展示规范 | [guidelines.md](guidelines.md) |
| 报表与看数 | [reporting.md](reporting.md) |

## 结算速记

PayPal、银行电汇等；常见满 **$100** 起付（以后台为准）。详见 [结算与收款](../../ops/payout.md)。

## 个人开发者检查清单

- [ ] Facebook / Meta 开发者账号可用  
- [ ] 应用已在支持的商店上架且链接可访问  
- [ ] 主聚合已配置 Meta Bidding（见 [via-mediation](via-mediation.md)），而非只拷了 AAR  
- [ ] [app-ads.txt](../../ops/ads-txt.md) / 授权状态无报错  
- [ ] [ATT / 同意与隐私](../../ops/privacy.md) 已按目标市场处理  
- [ ] 展示与激励交互符合 [guidelines](guidelines.md)

返回：[聚合策略](../../mediation/overview.md) · [官方平台对照](../../portals.md)
