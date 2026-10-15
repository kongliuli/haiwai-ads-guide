# LevelPlay · Android 原生 SDK（非 Unity）

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Android SDK integration](https://docs.unity.com/en-us/grow/levelplay/sdk/android/sdk-integration)  
> 本地材料：[materials/sdk/unity-levelplay/SOURCE.md](../../../materials/sdk/unity-levelplay/SOURCE.md)

面向**不用 Unity 引擎**、但仍想用 LevelPlay 聚合（含 Unity Ads 等网络）的 Android 个人开发者。Unity 工程请走 [Unity 包](unity-package.md)。

## 环境前提

- Android API 19+  
- Kotlin 最低常见要求：**1.7.0**（以官网为准）

## 1. 加入 LevelPlay SDK

### 推荐：Maven Central（Gradle）

仓库（Gradle 7+ 写在 `settings.gradle` 的 `dependencyResolutionManagement`）：

```groovy
repositories {
  mavenCentral()
}
```

依赖（版本以官网 / Maven 为准；本仓库归档过 **9.6.1**）：

```groovy
dependencies {
  implementation("com.unity3d.ads-mediation:mediation-sdk:9.6.1")
}
```

自 **8.9.0** 起，AdQuality 打进 LevelPlay，随初始化一起起来（细节见官网 AdQuality 文档）。

### 备选：手动 AAR

1. 下载 `mediation-sdk-x.y.z.aar`（本仓：`materials/sdk/unity-levelplay/mediation-sdk-9.6.1.aar`）  
2. 作为 module / `libs` 依赖导入  
3. 较新 SDK 通常还需要 Kotlin 标准库支持  

仅接 **Unity Ads 网络本体**（不做 LevelPlay 聚合）时，坐标是另一套：

```groovy
implementation("com.unity3d.ads:unity-ads:4.21.0")
```

多数个人开发者要聚合填充，应优先 **mediation-sdk**，再在 LevelPlay 后台配网络。

## 2. Google 标识相关依赖与权限

便于读取 GAID / App Set ID，常见再加：

```groovy
dependencies {
  implementation("com.google.android.gms:play-services-appset:16.0.0")
  implementation("com.google.android.gms:play-services-ads-identifier:18.1.0")
  implementation("com.google.android.gms:play-services-basement:18.1.0")
}
```

`targetSdk` 到 **33+** 时，在 Manifest 声明广告 ID 相关 normal permission（见官网原文）。**亚马逊设备**不走 Play Services，可跳过本步。

## 3. 初始化 SDK

在 LevelPlay 控制台创建应用，拿到 **appKey**。实现成功/失败监听后调用 `LevelPlay.init`：

```java
LevelPlayInitRequest initRequest = new LevelPlayInitRequest.Builder(appKey)
    .withUserId("UserID") // S2S 发奖或 Ad Quality 用户旅程时建议传
    .build();

LevelPlayInitListener initListener = new LevelPlayInitListener() {
    @Override
    public void onInitFailed(@NonNull LevelPlayInitError error) {
        // 建议稍后重试
    }

    @Override
    public void onInitSuccess(LevelPlayConfiguration configuration) {
        // 在此之后再创建并 load 广告
    }
};

LevelPlay.init(context, initRequest, initListener);
```

| 回调 | 含义 |
|------|------|
| `onInitSuccess` | 配置拉取成功，可创建/加载广告 |
| `onInitFailed` | 无法加载广告；网络恢复或原因消除后再 Init |

使用 ProGuard / R8 时，按官网粘贴 keep 规则（含适配器、OMID、各网络接口等），否则 release 包易出问题。

## 4. 验证集成

Init **之前**：

```java
LevelPlay.setMetaData("is_test_suite", "enable");
```

初始化成功后（需 Application Context）：

```java
LevelPlay.launchTestSuite(context);
```

官方另有 Integration Demo 工程，可对照完整接入。

## 5. 下一步

接一种广告格式先跑通：Rewarded Video / Interstitial / Banner / Native，再按 [Mediation Networks](mediation-networks.md) 思路在后台加竞价/瀑布网络。网络 Adapter 在原生 Android 侧通常通过各网络的 LevelPlay Android 集成页配置（与 Unity Network Manager 路径不同）。

## 常见坑

- 只加了 `unity-ads` AAR、却以为已经做了 LevelPlay 聚合  
- `targetSdk 33+` 未声明广告 ID 权限  
- ProGuard 未 keep 适配器 → 线上无填充  

返回：[概览](index.md) · [Unity 包](unity-package.md) · [Mediation Networks](mediation-networks.md)
