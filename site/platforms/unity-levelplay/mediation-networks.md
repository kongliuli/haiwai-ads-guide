# LevelPlay · 配置 Mediation Networks（含默认 Unity Ads）

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Mediation Networks for Unity](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/mediation-networks)  
> 本地材料：[materials/sdk/unity-levelplay/SOURCE.md](../../../materials/sdk/unity-levelplay/SOURCE.md)

在已能初始化 LevelPlay、并至少接好一种广告格式（激励 / 插屏 / 横幅）之后，用 **Mediation Networks** 把更多广告源接进同一条瀑布或 Bidding，提高填充与 eCPM。

本文以 **Unity 包 + Network Manager** 为主；原生 Android 请对照各网络的 LevelPlay Android 集成页加依赖。

## 前提

- 已完成 [Unity 包集成](unity-package.md)（或原生 [Android SDK](android-native.md)）  
- 应用内已按官方指南接好至少一种广告单元  
- 若接 AdMob：注意其较新 SDK 使用 **AndroidX**，工程需已迁移

## LevelPlay Network Manager（Unity）

1. 菜单：`Ads Mediation` → **Network Manager**  
2. 对目标网络点 **Install** 或 **Update**  
3. **Android**：改完后执行  
   `Assets` → `Mobile Dependency Manager` → `Android Resolver` → **Resolve**  
   （否则依赖不会落到工程 / Gradle）

每个网络装完 Adapter 后，还要在 **LevelPlay 控制台** 与该网络后台完成账号、Placement、Bidding 等配置——只装包不够。

## 默认：Unity Ads

- 自 LevelPlay Unity 包 **8.8.1** 起：默认安装 **Unity Ads adapter**（另有 ironSource Ads）  
- 自包 **9.0.0** 起：升级 LevelPlay 包时，Unity Ads adapter 会尽量自动跟到兼容的最新版  

个人游戏起步：先保证 **Unity Ads 在后台已开通、Placement 绑好**，用测试套件确认能出广告，再加 AdMob / Meta / AppLovin 等。

### 手动钉死 Unity Ads adapter 版本（少见）

1. 打开 `LevelPlay/Editor/ISUnityAdsAdapterDependencies.xml`  
2. 在 `<unityversion>…</unityversion>` 指定版本  
3. 核对同文件里 Android `<androidPackage spec="…">` 与 iOS `<iosPod version="…">` 与该 adapter 兼容  

本仓库归档的 Unity Ads Android SDK 参考坐标：`com.unity3d.ads:unity-ads:4.21.0`（以 adapter 要求为准）。

## 常用网络一览（版本会变，以官网表为准）

官网「Mediation Networks for Unity」维护一张大表（Adapter 版、网络 SDK 版、支持单元、Changelog）。个人开发者常优先考虑：

| 网络 | 常见用途 | 支持单元（官网表常见） |
|------|----------|------------------------|
| **Unity Ads** | Unity 游戏默认源 | Banner / Interstitial / Rewarded |
| Google AdMob / Ad Manager | 填充底仓 | 同上 |
| Meta Audience Network | Tier-1/2 画像 | 同上 |
| AppLovin | 激励/插屏竞价 | 同上 |
| Mintegral / Pangle / Liftoff Monetize 等 | 区域与玩法补充 | 见表 |

Adapter **自带该网络 SDK + 对接代码**，一般不必再单独硬接一份网络 SDK（除非该网络集成指南另有要求）。

完整名单与当前版本号请直接打开对照原文表格，本站不镜像逐行版本以免过期。

## 不用 Network Manager 时的手动接入

### 用 Adapter XML

1. 下载对应网络的 adapters XML  
2. 放到 `Assets/LevelPlay/Editor`（极旧 SDK 8.0.0 及更早可能是 `Assets/IronSource/Editor`）

### 直接丢 Android / iOS 产物

- Android：`.aar` / `.jar` → `Assets/Plugins/Android`  
- iOS：按下载包说明把 framework 等放进 `Assets/Plugins/iOS`  

仅在无法使用 Network Manager 时考虑；日常优先 Manager + Resolve。

## 验证

- Unity：用 [Integration Helper](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/integration-helper) / 集成测试套件  
- 确认目标网络在测试套件列表中可请求到广告  
- 控制台侧检查该网络是否 **Active**、Placement / Ad Unit 映射正确  

## 个人开发者建议顺序

1. LevelPlay Init + Unity Ads（默认 adapter）跑通激励或插屏  
2. 加 **AdMob**（底仓）  
3. DAU 起来后再加 **Meta AN**、**AppLovin** 等 Bidding 源，避免一上来装十几个网络却未在后台配齐  

返回：[概览](index.md) · [Unity 包](unity-package.md) · [Android 原生](android-native.md)
