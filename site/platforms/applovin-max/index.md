# AppLovin MAX · 概览与起步

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Getting started](https://support.applovin.com/en/max/getting-started) · [Android 集成](https://support.applovin.com/en/max/android/overview/integration) · [iOS 集成](https://support.applovin.com/en/max/ios/overview/integration) · 控制台 [dash.applovin.com](https://dash.applovin.com/) · 产品 [MAX](https://www.applovin.com/max/)

## 这是什么

MAX 是 AppLovin 的广告聚合与 Bidding 平台，在激励视频、插屏等格式上 eCPM 表现常年强势，适合游戏与中重度 App 作为**主聚合层**（也可与自有 AppLovin 网络一起用）。

官方文档平台：**AppLovin Support Center（MAX）** → [平台地图](portal-map.md)。

## 个人开发者要点

- 支持个人注册；部分高级能力可能需人工审核  
- 结算常见 PayPal、电汇；起付门槛随方式变化（文档/后台常见约 $20–$150）  
- 适合：已决定不以纯 AdMob 为唯一路径、或游戏向要冲激励 eCPM  
- 儿童向应用注意：AppLovin 不在 Families Self-Certified 名单（见 Getting started）

## 本站深页

| 页面 | 内容 |
|------|------|
| [平台地图](portal-map.md) | Support Center 栏目 ↔ 本站对照 |
| [Getting started 七步](getting-started.md) | 账号 → Ad Unit → SDK → 测试 → Connect → Waterfall → 报表 |
| [Android 集成加深](android.md) | 依赖、SDK Key、初始化 |
| [iOS 集成加深](ios.md) | CocoaPods / SPM、ATT / SKAdNetwork |
| [Preparing 网络](preparing-networks.md) | 勾选生成 adapter / Integration Manager |
| [Mediation 网络与 Bidding](networks-bidding.md) | 后台 Connect、Meta / Unity / Pangle / Mintegral |
| [Testing](testing.md) | Test mode、Mediation Debugger、Demo app |

## Getting started（摘要）

官方七步全文：[getting-started.md](getting-started.md)。最短路径：

1. 账号 + 付款 + Domain / `app-ads.txt`  
2. 控制台建 App 与 Ad Unit（每格式一 ID）  
3. 集成 MAX SDK + Preparing 挂网络  
4. Test mode / Debugger 验绿  
5. Networks Connect → Ad Unit Waterfall 开 Bidder  
6. Analyze 看 fill / win rate 再扩源  

## Android 起步（摘要）

`minSdkVersion` ≥ 24。加依赖后，用 `AppLovinSdkInitializationConfiguration` 传入 SDK Key 并 `setMediationProvider(MAX)`，在 Application / 启动 Activity 尽早 `initialize`。调试机把 GAID 写入 `setTestDeviceAdvertisingIds`。

```groovy
dependencies {
  implementation("com.applovin:applovin-sdk:+")
  // 或钉死版本，例如 13.6.4
}
```

细节与完整示例：[android.md](android.md)。## iOS 起步（摘要）

- CocoaPods：`pod 'AppLovinSDK'`，或 Xcode SPM  
- 最低 iOS 12、Xcode 15+（以官网为准）  
- `ALSdkInitializationConfiguration` + `ALMediationProviderMAX`，在 `didFinishLaunching` 初始化  
- 测试机写入 IDFA；上架前补 SKAdNetwork / ATT  

细节：[ios.md](ios.md)。源码型参考归档：`AppLovin-MAX-SDK-iOS-master.zip`（生产仍建议 Pod/SPM）。

## 加网络与测试（摘要）

1. 官网 Preparing 勾选生成依赖 → [preparing-networks.md](preparing-networks.md)  
2. 控制台 Connect + Ad Unit Bidder → [networks-bidding.md](networks-bidding.md)  
3. Test mode + Mediation Debugger → [testing.md](testing.md)  

## 与 AdMob Mediation 怎么选

| 你更在意 | 倾向 |
|----------|------|
| Google 账号一体、工具 App、已用 AdMob | AdMob Mediation |
| 游戏、激励/插屏收益、Bidding 体验 | MAX |

详见 [聚合策略](../../mediation/overview.md)。
