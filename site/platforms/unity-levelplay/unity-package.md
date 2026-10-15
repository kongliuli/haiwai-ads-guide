# LevelPlay · Unity 包安装与首次出广告

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Unity Package integration](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/package-integration)  

面向用 **Unity 引擎** 做游戏的个人开发者：把 LevelPlay（Ads Mediation）装进工程，初始化成功后即可接激励/插屏等格式。

## 环境前提

- Unity Editor：官方支持的 Supported / LTS 版本  
- Android：API 19+（4.4+）  
- iOS：LevelPlay 聚合侧常见要求 **iOS 13+**、**Xcode 16+**（各广告网络可能另有下限）  

从旧版升到 **9.0.0+** 时，请跟官网「升级指南」，不要只覆盖导入。

## 1. 安装 LevelPlay 包

**推荐：Package Manager**

1. `Window` → `Package Manager`  
2. 搜索 **Ads Mediation**，点 Install  
3. 或按包名添加：`com.unity.services.levelplay`

**备选：`.unitypackage`**

- 从官网下载当前 Unity Plugin（文档页会标版本，例如 9.x）  
- （版本可能落后于官网，以可跑通为准）

装好后，可在包详情的 **Samples** 里导入 **LevelPlay Sample**，用官方示例先摸清流程。

## 2. 控制台拿 App Key 并初始化

1. 打开 [LevelPlay / Unity Dashboard](https://dashboard.unity3d.com/)，创建应用  
2. 复制 **App Key**  
3. 在脚本里引入命名空间并初始化（**先注册回调，再 Init**）：

```csharp
using Unity.Services.LevelPlay;

public void Start()
{
    LevelPlay.OnInitSuccess += SdkInitializationCompletedEvent;
    LevelPlay.OnInitFailed += SdkInitializationFailedEvent;
    LevelPlay.Init("ThisIsYourAppKey");
    // 需要 Ad Quality 用户旅程或 S2S 发奖时：
    // LevelPlay.Init("ThisIsYourAppKey", "UserId");
}
```

| 回调 | 含义 |
|------|------|
| `OnInitSuccess` | 初始化成功，**之后再**创建/加载广告 |
| `OnInitFailed` | 失败则不会出广告；建议网络恢复或原因消除后再试 Init |

## 3. LevelPlay Network Manager

菜单：`Ads Mediation` → Network Manager，可用来：

- 更新 LevelPlay SDK  
- 安装 / 更新各广告网络 Adapter（装完还要在控制台与官方指引里分别配置）  
- 按已装网络自动维护 iOS `Info.plist` 的 SKAdNetwork ID  

自 **Unity 包 8.8.1** 起，除 ironSource Ads 外，**默认会安装 Unity Ads adapter**。Unity Ads 账号侧配置见官网 Unity Ads Integration Guide；本站深页见 [配置 Mediation Networks](mediation-networks.md)。

### Android 依赖解析

在 Network Manager 改完网络后，用 Mobile Dependency Manager 解析一次：

`Assets` → `Mobile Dependency Manager` → `Android Resolver` → `Resolve`

若希望产物进 Gradle 而不是下载进工程：开启 Custom Main Gradle Template，并在 Android Resolver Settings 勾选 **Patch mainTemplate.gradle**。较新包（如 9.1.0+ 全新安装）可能已自动处理。

### iOS 注意（摘要）

- **ATS**：顶层 `NSAppTransportSecurity` → `NSAllowsArbitraryLoads = YES`（勿叠一堆冲突例外）  
- **SKAdNetwork**：包 9.1.0+ 可自动管理；关闭自动化则须手写各网络 SKAN ID  
- 还需按 Apple 要求处理 **Privacy Manifest** 与应用侧隐私 API  

### Android 13+（API 33+）

Manifest 需声明 Google Play 广告 ID 相关 normal permission（详见官网；漏声明会影响 GAID）。

## 4. 用集成测试套件验证

初始化**之前**：

```csharp
LevelPlay.SetMetaData("is_test_suite", "enable");
```

`OnInitSuccess` 之后：

```csharp
LevelPlay.LaunchTestSuite();
```

用来检查 SDK、平台配置与已配网络能否拉到广告。

## 5. 下一步（出第一支广告）

集成包 + Init 成功后，按官网格式指南接一种即可先跑通，例如：

- Rewarded Video（游戏最常用）  
- Interstitial  
- Banner  

再按需加其他 mediation 网络（见 [mediation-networks.md](mediation-networks.md)）。

## 常见坑

- 先 Init 后注册回调 → 错过成功/失败事件  
- 改了 Network Manager 却未 Resolve → Android 缺依赖  
- 用正式单元在未上架环境狂刷 → 账号风险；先用测试套件 / 测试配置  

返回：[概览](index.md) · [Android 原生 LevelPlay](android-native.md) · [Mediation Networks](mediation-networks.md)
