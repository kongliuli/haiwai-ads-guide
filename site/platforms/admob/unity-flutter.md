# AdMob · Unity / Flutter 接入要点

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Unity Get started](https://developers.google.com/admob/unity/quick-start) · [Flutter Get started](https://developers.google.com/admob/flutter/quick-start) · 平台总入口 [AdMob for Developers](https://developers.google.com/admob)

原生 Android / iOS 仍是 AdMob 文档的主轴；**Unity** 与 **Flutter** 在同一文档站用平台切换进入，API 是对 Google Mobile Ads 的封装。概念（App ID、广告单元、测试 ID、UMP、Mediation）与原生一致，差别主要在**安装插件、生命周期钩子、导出工程配置**。

相关：[Android 起步](android-getting-started.md) · [iOS 起步](ios-getting-started.md) · [测试](testing.md) · [隐私 UMP](privacy-ump.md) · [栏目地图](portal-map.md)

---

## 1. 和原生共同的前置

无论 Unity 还是 Flutter：

1. 在 [AdMob 控制台](https://admob.google.com/) 创建应用，拿到 **App ID**（`ca-app-pub-…~…`）。  
2. 按格式创建 **广告单元**，开发期用[官方测试 Unit ID](testing.md)。  
3. 目标地区需要同意时，按 [隐私与 UMP](privacy-ump.md) 配置 Privacy & messaging，再在插件侧接 UMP API。  
4. 日活起来后再开 Mediation；Adapter 与导出后的 Gradle / Pod 配置要跟官方 Mediation 页走。

不要假设「只用 C# / Dart 就不用碰 AndroidManifest / Info.plist」——导出工程里仍要写入 App ID（或由官方插件/Gradle 脚本注入，以当前文档为准）。

---

## 2. Unity

### 官方入口（按需点进）

| 主题 | 官方 |
|------|------|
| 快速开始 | https://developers.google.com/admob/unity/quick-start |
| 测试广告 | https://developers.google.com/admob/unity/test-ads |
| 各广告格式 | 文档站 Unity 树下 banner / interstitial / rewarded 等 |
| 隐私 / UMP | https://developers.google.com/admob/unity/privacy |
| Mediation | https://developers.google.com/admob/unity/mediation |

### 接入要点（中文摘要）

- **安装**：按 quick-start 导入 Google Mobile Ads Unity 插件（Package Manager / `.unitypackage` 以官网当前方式为准），并满足最低 Unity 版本。  
- **App ID**：在插件设置或 `GoogleMobileAdsSettings`（名称以版本为准）填 Android / iOS 各自的 App ID；导出后核对 Gradle 与 Xcode 工程是否写到。  
- **初始化**：在加载广告前调用官方 `MobileAds.Initialize`（或现行 API）；有 Mediation 时等初始化回调再 load。  
- **线程与场景**：广告回调可能不在你预期的主线程/场景时机；UI 与发奖逻辑切回 Unity 主线程，避免在回调里直接改场景对象翻车。  
- **激励发奖**：以 Rewarded 回调的「用户应获得奖励」为准，服务端校验另说；勿仅凭「广告关闭」发奖。  
- **导出**：IL2CPP、minSdk、iOS bitcode/ATT 文案等跟官方与商店要求对齐；Mediation 源常要在导出工程里加额外依赖。

若游戏同时考虑 Unity Ads / LevelPlay 做**主聚合**，那是另一条产品线——见本站 [Unity LevelPlay](../unity-levelplay/index.md)。**不要** AdMob Mediation 与 MAX/LevelPlay 双主聚合叠罗汉。

---

## 3. Flutter

### 官方入口（按需点进）

| 主题 | 官方 |
|------|------|
| 快速开始 | https://developers.google.com/admob/flutter/quick-start |
| 测试广告 | https://developers.google.com/admob/flutter/test-ads |
| 各广告格式 | 文档站 Flutter 树下各 format 页 |
| 隐私 / UMP | https://developers.google.com/admob/flutter/privacy |
| Mediation | https://developers.google.com/admob/flutter/mediation |

### 接入要点（中文摘要）

- **插件**：使用官方文档指定的 `google_mobile_ads`（包名以 pub.dev / 官网为准），锁定与文档一致的版本区间。  
- **平台文件**：  
  - Android：`AndroidManifest.xml` 写入 `APPLICATION_ID` meta-data。  
  - iOS：`Info.plist` 写入 `GADApplicationIdentifier`（键名以现行文档为准）。  
- **初始化**：在 `runApp` 前后按文档 `MobileAds.instance.initialize()`；同意流程完成前谨慎请求广告。  
- **Widget 生命周期**：Banner 等需正确 `dispose`；路由切换时避免泄漏与重复 load。  
- **插屏 / 激励**：在用户操作或自然断点触发，注意与 Navigator 的时序；`load` 与 `show` 拆开，失败要可重试且有上限。  
- **热重载**：广告 SDK 对热重载不友好；验证展示与回调用**完全重启**。

---

## 4. 测试与隐私（跨引擎）

- 测试 Unit ID、测试设备规则与原生相同 → [testing.md](testing.md)。  
- UMP：控制台消息 + 引擎侧 privacy API → [privacy-ump.md](privacy-ump.md)；清单 → [ops/privacy.md](../../ops/privacy.md)。  
- iOS ATT：在导出的 Xcode 工程配置用途说明字符串；Flutter/Unity 都可能要用平台通道或官方插件封装来请求授权。

---

## 5. 怎么选文档深度

| 你的情况 | 建议 |
|----------|------|
| 会原生、临时导 Unity/Flutter | 先读本页 + 官方 quick-start，格式细节回官方该平台页 |
| 纯引擎开发、少碰原生 | 官方 Unity/Flutter 树为主；本站 [formats](formats.md) / [mediation](mediation.md) 补产品决策 |
| 只要 Web 站赚钱 | AdMob 不是主路径 → 看 [AdSense](../adsense/index.md) |

单格式（如 Flutter Rewarded）的逐步代码以官网为准；本站不镜像粘贴大段 SDK 示例，避免与版本脱节。

返回 [AdMob 概览](index.md) · [栏目地图](portal-map.md)
