# Meta AN · 经聚合 Bidding 接入

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Audience Network](https://developers.facebook.com/docs/audience-network) · AdMob [Android Meta Bidding](https://developers.google.com/admob/android/mediation/meta) / [iOS](https://developers.google.com/admob/ios/mediation/meta) · MAX [SDK bidder 指南](https://support.applovin.com/en/max/mediated-network-guides/sdk-bidder-network-guides) · LevelPlay [Unity Meta](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/networks/guides/meta-audience-network) / [Android](https://docs.unity.com/en-us/grow/levelplay/sdk/android/networks/guides/meta-audience-network) / [iOS](https://docs.unity.com/en-us/grow/levelplay/sdk/ios/networks/guides/meta-audience-network)

面向个人开发者：把 Meta Audience Network 当作**竞价广告源**接到已有主聚合（AdMob / MAX / LevelPlay），而不是长期单独直连 SDK。Meta 自 2021 年起对 Mediation 以 **Bidding only** 为主；生产路径请以各平台当前文档为准。

## 为什么走聚合

| 直连 SDK | 经聚合 Bidding |
|----------|----------------|
| 自己管请求、填充、比价 | 主聚合统一拍卖，Meta 与其它源实时竞价 |
| 包体与初始化单独维护 | 跟主聚合 SDK + Meta adapter 一起升 |
| 难与 AdMob/MAX 等并存 | 个人默认推荐路径 |

先选定**唯一主聚合层**（见 [聚合策略](../../mediation/overview.md)），再开 Meta。

## 通用实操清单

按顺序做；任一步卡住时先查对应控制台状态，再查官方 adapter 页。

### 1. 账号与权益

- [ ] 可用的 Facebook / Meta 个人或开发者账号  
- [ ] 在 [Monetization Manager](https://business.facebook.com/) / Audience Network 侧完成发布者/商务设置  
- [ ] 已添加收款信息（无 payout 往往收不到 AN 广告）  
- [ ] 若聚合要求「Login with Facebook / 签署 Bidding 合作」，在聚合后台点完 Acknowledge & agree  

### 2. 应用与商店链接

- [ ] App 已在 Google Play 和/或 App Store 上架（或平台当前允许的测试态）  
- [ ] 商店详情里的**开发者网站**可访问，且与 [app-ads.txt](../../ops/ads-txt.md) 域名一致  
- [ ] Meta 侧 Property / 应用与商店包名、Bundle ID 一致，无「未授权 / 链接无效」类报错  

### 3. Meta 侧广告位

- [ ] 在 Monetization Manager 为该 Property 创建 Placement  
- [ ] 格式与聚合广告位一致（Banner / Interstitial / Rewarded / Native 等）  
- [ ] 复制 **Placement ID**（及平台要求的 App ID）备填到聚合后台  

### 4. 聚合后台映射

- [ ] 在主聚合的广告单元上启用 Meta Audience Network（Bidding）  
- [ ] 填入 Placement ID（LevelPlay 等还可能要 App ID）  
- [ ] 状态为 Active / 参与竞价，而非仅挂了 adapter 未映射  

### 5. 工程：SDK + adapter

- [ ] 主聚合 SDK 版本满足 Meta bidding 最低要求  
- [ ] 引入官方 **Meta / Facebook mediation adapter**（不要只拷 AAR 却不配后台）  
- [ ] iOS：`setAdvertiserTrackingEnabled`、SKAdNetwork ID、ATT 与隐私链路就绪（见 [隐私合规](../../ops/privacy.md)）  
- [ ] 用各平台**测试模式 / 测试设备**验证能出 Meta 测试广告或至少能进竞价日志  

### 6. 上线后核对

- [ ] app-ads.txt / ads.txt 含 Meta 要求的授权行（控制台常给片段）  
- [ ] 无账号冻结、支付 hold、商店链接失效  
- [ ] 报表里能看到 Meta 作为 bidding 源的展示/收益（冷启动可能延迟）  

---

## 按主聚合拆分

### A. AdMob Mediation

1. Meta Monetization Manager 建 Property + Placement，拿到 Placement ID。  
2. AdMob 控制台 → 广告单元 → Mediation → **Bidding** → 添加 **Meta Audience Network** → 签署合作 → 映射 Placement ID。  
3. App 依赖：Google Mobile Ads SDK + `com.google.ads.mediation:facebook`（版本以文档为准）。  
4. 用 AdMob 测试广告单元 / 测试设备验证。

官方入口：

| 平台 | 链接 |
|------|------|
| Android | [Integrate Meta with bidding](https://developers.google.com/admob/android/mediation/meta) |
| iOS | [Integrate Meta with bidding](https://developers.google.com/admob/ios/mediation/meta) |
| Flutter | [Flutter · Meta](https://developers.google.com/admob/flutter/mediation/meta) |
| 可选广告源总表 | [Choose ad sources](https://developers.google.com/admob/android/choose-networks) |

### B. AppLovin MAX

1. Meta 侧建 Property / Placement，复制 Placement ID。  
2. MAX 控制台 → Ad Units → 对应单元 → 启用 Meta Audience Network，粘贴 Placement ID 并 Save。  
3. 工程引入 MAX SDK + Meta adapter（Android Maven / iOS CocoaPods `AppLovinMediationFacebookAdapter` 或 [SPM Meta 包](https://github.com/AppLovin/AppLovin-MAX-Swift-Package-Meta)）。  
4. 用 MAX 测试模式验证；确认 Meta 收款信息已填。

官方入口：

| 主题 | 链接 |
|------|------|
| SDK bidder 网络指南（含 Meta） | [sdk-bidder-network-guides](https://support.applovin.com/en/max/mediated-network-guides/sdk-bidder-network-guides) |
| iOS 准备 mediated networks | [preparing-mediated-networks](https://support.applovin.com/en/max/ios/preparing-mediated-networks) |
| Meta 文档站（Audience Network） | [developers.facebook.com/docs/audience-network](https://developers.facebook.com/docs/audience-network) |

### C. Unity LevelPlay

1. Meta 账号可用；LevelPlay → SDK Networks → Meta → **Login with Facebook**（按后台指引）。  
2. App 级填 Meta **App ID**；广告单元/实例级填完整 **Placement ID**。  
3. LevelPlay SDK ≥ 文档要求的 bidding 版本（Meta bidding 常见要求 SDK 6.11.0+，以当前文档为准）。  
4. 用 Network Manager / 对应平台依赖安装 Meta adapter，再测激励/插屏等。

官方入口：

| 平台 | 链接 |
|------|------|
| Unity | [Meta Audience Network integration](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/networks/guides/meta-audience-network) |
| Android | [Meta · Android](https://docs.unity.com/en-us/grow/levelplay/sdk/android/networks/guides/meta-audience-network) |
| iOS | [Meta · iOS](https://docs.unity.com/en-us/grow/levelplay/sdk/ios/networks/guides/meta-audience-network) |
| In-app bidding 概念 | [In-app bidding](https://docs.unity.com/en-us/grow/levelplay/platform/fundamentals/in-app-bidding) |

---

## 测试时注意

- 测试设备 / 测试模式开着时，不要用生产收益做结论。  
- 「没填充」先查：映射 ID 是否贴错、adapter 是否进包、商店链接与 app-ads.txt、Meta 账号是否可付。  
- Bidding 源无固定「瀑布 eCPM 档位」可调——比的是实时出价，不是手工 waterfall floor。

## 相关页

- [Meta AN 概览](index.md)  
- [聚合策略](../../mediation/overview.md)  
- [app-ads.txt](../../ops/ads-txt.md) · [隐私](../../ops/privacy.md) · [结算](../../ops/payout.md)
