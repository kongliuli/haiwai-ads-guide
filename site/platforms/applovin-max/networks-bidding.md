# AppLovin MAX · 添加 Mediation 网络与 Bidding

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Getting started](https://support.applovin.com/en/max/getting-started) · [SDK bidder network guides](https://support.applovin.com/en/max/mediated-network-guides/sdk-bidder-network-guides) · [Preparing mediated networks · Android](https://support.applovin.com/en/max/android/preparing-mediated-networks) · [Preparing mediated networks · iOS](https://support.applovin.com/en/max/ios/preparing-mediated-networks) · [Enable networks](https://support.applovin.com/en/max/getting-started)（控制台 Connect Networks 段）

核心 SDK 跑通后（[Android](android.md) / [iOS](ios.md)），收益主要来自**多家 Bidding 源同场竞价**。本页讲后台怎么连、工程里怎么挂 adapter，以及个人开发者常踩的版本坑。

## 总体流程（建议顺序）

1. 各广告网络官网注册、过审、建 App / Placement（尽量为 MAX **单独**建一套 ID，报表更干净）  
2. 工程加入对应 **MAX mediation adapter**（Gradle / Pod；POM/Pod 常会拉上网络自家 SDK）  
3. MAX 控制台：**MAX → Mediation → Manage → Networks** 点 Connect，填 API Key / 账号凭证  
4. 打开某个 **Ad Unit → Default Waterfall**：在 Bidder 区打开该网络，填 Placement / Game ID 等，Status 打开并 Save  
5. 用 **Mediation Debugger + Test Mode** 验绿，再放量  

官方总览七步见 [Getting started](https://support.applovin.com/en/max/getting-started)。起步阶段官网建议除 AppLovin 外再接约 **6 家**有全球需求的源（如 Google、Meta）；个人量小时可先 3–4 家 Bidding，再按报表扩。

## 控制台：Connect Networks vs Ad Unit Waterfall

| 位置 | 做什么 |
|------|--------|
| **Manage → Networks** | 账号级连接：API Key、报表拉取、Bidding 资格；成功多为绿色勾 |
| **Manage → Ad Units → 某广告位** | 该位是否启用该网络、填 Placement ID、Bidder vs 传统 waterfall |

只 Connect 却不在广告位 Status 打开 → 工程里有 adapter 也**不会**参与该位竞价。自定义 Custom Network 一般**不能**进 in-app bidding / auto-CPM。

优先开 **Bidder Networks**；传统 waterfall 要手填 CPM，维护成本高。

## 工程：挂 adapter（示例）

以个人开发者常开的四家为例。完整勾选列表与仓库 URL 以官网 Preparing 页为准（页面勾选后会生成定制 Gradle / Pod 片段）。

### Android（Gradle）

部分网络要额外 `maven { url "…" }`，例如 Mintegral 海外仓、Pangle（ByteDance）仓：

```groovy
repositories {
  google()
  mavenCentral()
  maven { url "https://dl-maven-android.mintegral.com/repository/mbridge_android_sdk_oversea" }
  maven { url "https://artifact.bytedance.com/repository/pangle" }
  // 其他网络按 Preparing 页追加
}

dependencies {
  implementation("com.applovin:applovin-sdk:+")
  implementation("com.applovin.mediation:facebook-adapter:+")   // Meta AN
  implementation("com.applovin.mediation:unityads-adapter:+")  // Unity Ads
  implementation("com.applovin.mediation:bytedance-adapter:+") // Pangle
  implementation("com.applovin.mediation:mintegral-adapter:+")  // Mintegral
}
```

推荐用 adapter 的 `+` / 文档指定版本，让 POM **自动**带上网络 SDK；不要改 adapter 包名，否则 MAX 认不出。开源 adapter 见 [AppLovin-MAX-SDK-Android](https://github.com/AppLovin/AppLovin-MAX-SDK-Android)，需自管网络 SDK。

### iOS

在 Preparing mediated networks（iOS）勾选同样网络后，按生成的 `pod` 行加入 Podfile（常见形态为 `AppLovinMediation*Adapter`），再 `pod install --repo-update`。SPM / 手动路径见该页。

## 各网络要点（Bidding）

明细步骤、字段名以 [SDK bidder network guides](https://support.applovin.com/en/max/mediated-network-guides/sdk-bidder-network-guides) 各章为准；下表只抓个人开发者最容易漏的。

### Meta Audience Network

- 需 Meta for Developers / Monetization；**付款信息**未配齐时往往无填充  
- 为 MAX 新建 Placement（或复用，但 Bidding 时 floor 行为与瀑布不同，按账号团队建议）  
- MAX 广告位里填 Meta Placement ID，打开 Status  
- Adapter：`facebook-adapter`（Android）/ 对应 iOS mediation pod  
- 加州等「Limited Data Use」等旗标按 Meta 与 MAX Privacy 文档传递  

本站：[Meta AN 概览](../meta-an/index.md)

### Unity Ads

- Bidding 对 **adapter 版本有下限**：插屏 / 激励常见需 **≥ 4.6.0.0**；Banner / MREC 常见需 **≥ 4.9.2.1**（以 bidder 指南当前句为准）  
- Monetization 控制台为 Bidding 自动生成各端 Placement；旧项目可按文档一键生成六套 Bidding placement  
- MAX 广告位填 **Game ID + Placement ID**  

本站：[Unity / LevelPlay 概览](../unity-levelplay/index.md)（此处 Unity Ads 是作为 **MAX 的广告源**，不是把 LevelPlay 当第二主聚合）

### Pangle（穿山甲海外）

- 在 Pangle 后台建 App 与 Placement，记下 App ID、Placement ID 填入 MAX  
- Android 通常要加 ByteDance Maven 仓 + `bytedance-adapter`  
- **版本注意**：较新的 Pangle iOS adapter（文档举例自 **4.9.1.0.0** 起）**不再服务中国大陆**；大陆流量需配 **CSJ** 与 CSJ adapter，海外继续用 Pangle。混区包务必分清  

### Mintegral

- 后台建 App / Unit 时 Bidding Type 选 **Header Bidding**（若选项灰掉，找 Mintegral 开通）  
- MAX 侧支持 Banner、激励、插屏、原生；其他 Mintegral 格式不要指望经 MAX 出  
- Android 需 Mintegral **海外** Maven 仓 + `mintegral-adapter`  
- 未配收款信息时可能无 fill  

## Adapter 版本怎么盯

1. **Mediation Debugger**：标红的「网络 SDK ↔ adapter」不匹配优先修  
2. Preparing 页 / Maven / CocoaPods 的 changelog：升 MAX 核心 SDK 时常要**整组**升 adapter  
3. 个别 Bidding（如上文 Unity、部分新网络）写死了**最低 adapter / 最低 MAX SDK**——低于下限等于白接  
4. 从 AdMob Mediation 等迁到 MAX：官网明确提醒勿复用旧 mediator 的 App ID 配置，易崩溃与报表错乱；尽量新建应用 ID 或清掉旧 Mediation Group  

包体与启动耗时随 adapter 线性涨：先看 Advanced Reporting 里 win rate / 收入，砍掉长期零贡献源。

## Support Center 入口（收藏）

| 用途 | 链接 |
|------|------|
| 七步总览（含 Connect / Waterfall） | https://support.applovin.com/en/max/getting-started |
| 各 Bidding 网络逐步指南 | https://support.applovin.com/en/max/mediated-network-guides/sdk-bidder-network-guides |
| Android 勾选生成依赖 | https://support.applovin.com/en/max/android/preparing-mediated-networks |
| iOS 勾选生成依赖 | https://support.applovin.com/en/max/ios/preparing-mediated-networks |
| Android / iOS Test mode | [Android](https://support.applovin.com/en/max/android/testing-networks/test-mode) · [iOS](https://support.applovin.com/en/max/ios/testing-networks/test-mode) |
| Mediation Debugger | 同平台 Testing networks → Mediation Debugger |
| MAX 控制台 | https://dash.applovin.com/ |

策略层讨论见 [聚合总论](../../mediation/overview.md)。

返回：[MAX 概览](index.md) · [Android](android.md) · [iOS](ios.md)
