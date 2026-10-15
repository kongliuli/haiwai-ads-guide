# Unity Ads / LevelPlay · 概览与起步

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Unity LevelPlay](https://docs.unity.com/en-us/grow/levelplay) · [Platform](https://docs.unity.com/en-us/grow/levelplay/platform) · [SDK](https://docs.unity.com/en-us/grow/levelplay/sdk) · [Account](https://docs.unity.com/en-us/grow/levelplay/account) · Dashboard [dashboard.unity3d.com](https://dashboard.unity3d.com/)  

## 名称怎么区分

| 名称 | 角色 |
|------|------|
| **Unity Ads** | 广告网络（尤其游戏激励视频） |
| **LevelPlay** | 聚合层（原 ironSource Mediation；现归 Unity Grow） |

个人用 Unity 做游戏时：注册 Unity ID → Dashboard 开变现 → 用 LevelPlay 包同时带上 Unity Ads 等网络，是常见路径。

官方文档平台分 **Platform / SDK / Account** 三块，栏目对照见 [portal-map.md](portal-map.md)。

## 本站分篇

| 页面 | 内容 |
|------|------|
| [官方文档平台地图](portal-map.md) | Platform / SDK / Account 栏目 ↔ 本站进度 |
| [控制台 / 广告位 / 应用配置](platform-basics.md) | New App、Ad units、Placements、频控 |
| [Unity 包 / Ads Mediation](unity-package.md) | Package Manager 或 `.unitypackage`、Init、Network Manager |
| [Android 原生 LevelPlay](android-native.md) | Maven `mediation-sdk`、GAID、Init、非 Unity 工程 |
| [配置 Mediation Networks](mediation-networks.md) | 装 Adapter（含默认 Unity Ads）、常用网络顺序 |
| [集成验证与测试套件](testing.md) | Integration Helper、Test Suite、Test devices |
| [报表要点](reporting.md) | Performance / 定时报表 / 怎么读数 |

## Unity 引擎侧起步（摘要）

推荐 Package Manager 安装 **Ads Mediation**：

- 包名：`com.unity.services.levelplay`  
- 或导入官方 `.unitypackage`  

自较新 LevelPlay Unity 包起，**默认会带 Unity Ads adapter**。详细步骤见 [unity-package.md](unity-package.md)。

## 原生 Android（摘要）

```groovy
repositories { mavenCentral() }
dependencies {
  implementation("com.unity3d.ads-mediation:mediation-sdk:9.6.1")
}
```

仅接 Unity Ads 网络本体时可用 `com.unity3d.ads:unity-ads:4.21.0`。完整步骤见 [android-native.md](android-native.md)。

## 控制台最小路径

1. [platform-basics](platform-basics.md)：建应用 → 拿 App Key → 激活广告单元  
2. 客户端 Init + 一种格式  
3. [testing](testing.md) 验证后再加网络与看 [reporting](reporting.md)

## 结算速记

常见电汇、PayPal；起付线多见 **$100**（以后台为准）。账号权限见官网 [Account](https://docs.unity.com/en-us/grow/levelplay/account)。

## 建议

- Unity 项目：主聚合优先 **LevelPlay**  
- 非 Unity 但仍想要游戏广告主池：可把 Unity Ads 作为 AdMob/MAX 的一个 Bidding 源  

返回：[聚合策略](../../mediation/overview.md) · [平台总览](../overview.md) · [portals](../../portals.md)
