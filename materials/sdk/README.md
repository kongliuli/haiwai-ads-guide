# SDK 预备材料索引（第二批）

> 编写模型: Composer (Cursor Agent) · 2026-10-15

本目录归档第一批五平台对应的**官网、文档入口、SDK 获取方式**，以及可落地的本地包（能直接下载的已收入子目录；仅走 Maven/CocoaPods/SPM 的写入坐标与说明）。

> 说明：正文平台表为 5 行；「Unity Ads」与「LevelPlay」分列入口，故本节按 **6 个接入入口** 登记。

## 总表

| # | 入口 | 官网 / 控制台 | SDK / 接入文档 | 本地目录 |
|---|------|---------------|----------------|----------|
| 1 | Google AdMob | https://admob.google.com/ | https://developers.google.com/admob | `admob/` |
| 2 | Google AdSense | https://www.google.com/adsense/ | https://support.google.com/adsense | `adsense/` |
| 3 | AppLovin MAX | https://www.applovin.com/max/ · 控制台 https://dash.applovin.com/ | https://support.applovin.com/hc/en-us/categories/360002372914 | `applovin-max/` |
| 4 | Unity Ads | https://unity.com/products/unity-ads · 控制台 https://dashboard.unity3d.com/ | https://docs.unity.com/ads | `unity-levelplay/`（同目录注明） |
| 5 | Unity LevelPlay | https://unity.com/products/levelplay · Grow 文档 https://docs.unity.com/grow/levelplay | https://docs.unity.com/en-us/grow/levelplay/sdk | `unity-levelplay/` |
| 6 | Meta Audience Network | https://www.facebook.com/audiencenetwork · 开发者 https://developers.facebook.com/docs/audience-network | Android / iOS 文档见下 | `meta-audience-network/` |

---

## 1. Google AdMob（Google Mobile Ads SDK）

| 项 | 链接 |
|----|------|
| 控制台 | https://admob.google.com/ |
| 开发者总览 | https://developers.google.com/admob |
| Android 快速开始（Legacy） | https://developers.google.com/admob/android/quick-start |
| Android 下载页 | https://developers.google.com/admob/android/download |
| iOS 下载页 | https://developers.google.com/admob/ios/download |
| iOS 手动包名 | `googlemobileadssdkios.zip`（版本以下载页为准，当前文档常见 **13.11.0**） |

**推荐集成方式**

- Android（Gradle）：`implementation("com.google.android.gms:play-services-ads:25.5.0")`（版本随官网更新）
- iOS：CocoaPods `Google-Mobile-Ads-SDK`，或下载页 ZIP / SPM

**本地下载策略**：Android 以 Maven 坐标为准（无独立「全家桶 zip」）；iOS 尽量拉取官方 ZIP。见 `admob/`。

---

## 2. Google AdSense（Web · 无传统原生 SDK）

| 项 | 链接 |
|----|------|
| 控制台 | https://www.google.com/adsense/ |
| 广告代码说明 | https://support.google.com/adsense/answer/9274634 |
| 放置位置 | https://support.google.com/adsense/answer/9190028 |

**接入脚本（官方 CDN）**

```text
https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-XXXXXXXX
```

本地仅保存示例片段与说明，见 `adsense/`（不镜像整站 JS 运行时依赖）。

---

## 3. AppLovin MAX

| 项 | 链接 |
|----|------|
| 产品页 | https://www.applovin.com/max/ |
| 控制台 | https://dash.applovin.com/ |
| Android 集成 | https://support.applovin.com/en/max/android/overview/integration |
| Android 手动集成 / 各网络包 | https://support.applovin.com/en/max/android/overview/manual-integration |
| iOS 集成 | https://support.applovin.com/en/max/ios/overview/integration |
| Android GitHub | https://github.com/AppLovin/AppLovin-MAX-SDK-Android |
| iOS GitHub | https://github.com/AppLovin/AppLovin-MAX-SDK-iOS |

**推荐集成方式**

- Android：`implementation 'com.applovin:applovin-sdk:+'`
- iOS：CocoaPods `pod 'AppLovinSDK'` 或 SPM

**本地下载**：优先 GitHub Releases / Maven 拉取核心 AAR，见 `applovin-max/`。

---

## 4–5. Unity Ads / LevelPlay

| 项 | 链接 |
|----|------|
| Unity Ads 产品 | https://unity.com/products/unity-ads |
| LevelPlay 产品 | https://unity.com/products/levelplay |
| Unity Dashboard | https://dashboard.unity3d.com/ |
| LevelPlay Unity 包集成 | https://docs.unity.com/en-us/grow/levelplay/sdk/unity/package-integration |
| LevelPlay Android | https://docs.unity.com/en-us/grow/levelplay/sdk/android/sdk-integration |
| Unity SDK GitHub Releases | https://github.com/ironsource-mobile/Unity-sdk/releases |

**推荐集成方式**

- Unity：Package Manager → `com.unity.services.levelplay`（Ads Mediation），或导入 `.unitypackage`
- 自 LevelPlay Unity 包 8.8.1+ 起，默认含 Unity Ads adapter

**本地下载**：`.unitypackage` 与 Android AAR（若可得），见 `unity-levelplay/`。

---

## 6. Meta Audience Network

| 项 | 链接 |
|----|------|
| 产品介绍 | https://www.facebook.com/audiencenetwork |
| 开发者文档 | https://developers.facebook.com/docs/audience-network |
| Android 加 SDK | https://developers.facebook.com/docs/audience-network/setting-up/platform-setup/android/add-sdk |
| iOS GitHub（SPM） | https://github.com/facebook/FBAudienceNetwork |
| iOS Releases | https://github.com/facebook/FBAudienceNetwork/releases |

**推荐集成方式**

- Android（Maven）：`com.facebook.android:audience-network-sdk`（版本以文档为准）
- iOS：Swift Package Manager → `https://github.com/facebook/FBAudienceNetwork`（CocoaPods 已逐步弃用）
- **生产建议**：经 AdMob / MAX / LevelPlay 的 Bidding 接入，而非长期单独直连

**本地下载**：iOS release 资产 + Android Maven 坐标说明，见 `meta-audience-network/`。

---

## 下载批次记录（2026-10-15）

| 入口 | 本地关键制品 | 状态 |
|------|--------------|------|
| AdMob | `admob/googlemobileadssdkios.zip`、`play-services-ads-25.5.0.aar` | 已落盘 |
| AdSense | `adsense/adsense-sample.html` | 示例片段（无原生 SDK） |
| AppLovin MAX | `applovin-max/applovin-sdk-13.6.4.aar` + iOS 仓库 zip | 已落盘 |
| Unity Ads | `unity-levelplay/unity-ads-4.21.0.aar` | 已落盘 |
| LevelPlay | `UnityLevelPlay_v9.3.0.unitypackage`、`mediation-sdk-9.6.1.aar` | 已落盘 |
| Meta AN | `audience-network-sdk-6.22.0.aar` | Android 已落盘；iOS 请走 SPM |

细节与直链见各子目录 `SOURCE.md`；总状态见 [docs/PENDING.md](../../docs/PENDING.md)。
