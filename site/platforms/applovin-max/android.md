# AppLovin MAX · Android 集成加深

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Android Integration](https://support.applovin.com/en/max/android/overview/integration) · [Test mode](https://support.applovin.com/en/max/android/testing-networks/test-mode) · [Mediation Debugger](https://support.applovin.com/en/max/android/testing-networks/mediation-debugger) · [Preparing mediated networks](https://support.applovin.com/en/max/android/preparing-mediated-networks)  

面向个人开发者：先把 **依赖 → SDK Key → 尽早初始化 → 测试模式** 跑通，再开 [Mediation / Bidding](networks-bidding.md)。

## 1. 工程前提

- `minSdkVersion` **≥ 24**（官网当前要求）  
- 仓库含 `google()` 与 `mavenCentral()`  
- 控制台 [dash.applovin.com](https://dash.applovin.com/) 已建应用与广告位；**SDK Key** 在 Account → General → Keys  
- 需要 AAID 时，按需引入 `play-services-ads-identifier`（见官网 Google Play services 说明）

发布更新可关注 [AppLovin-MAX-SDK-Android](https://github.com/AppLovin/AppLovin-MAX-SDK-Android)。

## 2. 加依赖

app 模块：

```groovy
dependencies {
  implementation("com.applovin:applovin-sdk:+")
  // 或钉死具体版本，例如 com.applovin:applovin-sdk:13.6.4
}
```

- ProGuard：MAX SDK / adapter 的 AAR 已带规则，一般**不必**再手写一份  
- 后续每个 Bidding 网络再加对应 `com.applovin.mediation:*-adapter:+`（及部分网络自有 Maven 仓），见 [networks-bidding.md](networks-bidding.md)。

### （可选）Ad Review

要在后台审创意时，根工程加 Quality Service 插件仓库与 classpath，app 模块 `apply plugin: 'applovin-quality-service'`，并把 Account → Keys 里的 **Ad Review Key** 写入 `applovin { apiKey "…" }`。细节以 [Integration](https://support.applovin.com/en/max/android/overview/integration) 页为准。

## 3. SDK Key 放哪里

当前文档主路径：在 **初始化配置**里传入 SDK Key（不再依赖旧式 Manifest `meta-data` 作为唯一写法）：

```kotlin
val initConfig = AppLovinSdkInitializationConfiguration.builder("YOUR_SDK_KEY")
  .setMediationProvider(AppLovinMediationProvider.MAX)
  .build()
```

Key 在 Account → General → Keys。上架包勿把测试专用逻辑留在 Release。

## 4. 初始化（尽早）

在 Application 或启动 Activity 的 `onCreate` 尽早调用，给各网络缓存广告留出时间：

```kotlin
AppLovinSdk.getInstance(this).initialize(initConfig) { _ ->
  // 初始化完成后再 load 插屏 / 激励等
}
```

初始化配置里的 mediationProvider、测试设备列表等大多是**创建时定死**的；`AppLovinSdkSettings`（用户 ID、隐私流程 URI 等）可在生命周期内再改。

个人开发者常用可选设置（按需）：

- `userIdentifier`：与自家账号体系对齐，便于排查  
- Terms & Privacy Policy Flow：挂上隐私政策 / 服务条款 URL（合规地区更稳）  
- Segment 等高级字段：无明确需求可先跳过

## 5. 测试模式与 Mediation Debugger

测试广告**不计**展示 / 点击 / 收入，只用来验集成。

### 代码打开（推荐调试机）

把本机 **GAID** 写入首次初始化配置：

```kotlin
val initConfig = AppLovinSdkInitializationConfiguration.builder("YOUR_SDK_KEY")
  .setMediationProvider(AppLovinMediationProvider.MAX)
  .setTestDeviceAdvertisingIds(listOf("YOUR_GAID"))
  .build()
```

日志初始化段出现 `Test Mode On: true` 即生效。测试期无填充时，可再试 live；无 fill 本身不一定代表集成坏了。

### Mediation Debugger

初始化后可用官方 Debugger 看各网络 adapter 是否装齐、版本是否匹配，并对单个网络开 Test Ad。路径见 [Mediation Debugger](https://support.applovin.com/en/max/android/testing-networks/mediation-debugger)。Debug 包留入口即可，正式用户勿默认弹出。

## 6. 接广告格式之前

1. 控制台建好对应格式的 Ad Unit ID  
2. 初始化回调后再 `load`  
3. 插屏 / 激励：失败重试（指数退避）+ 关闭后立刻预加载下一支（官网 Getting started 清单）  
4. Banner / MREC：尽量常驻可视区域，刷新率交给 MAX  

格式细节见 Support Center → Android → Ad formats。

## 常见坑

| 现象 | 优先检查 |
|------|----------|
| 初始化后无广告 | Key 是否正式；是否过早 load；网络 adapter 未加 |
| `Test Mode On: false` | GAID 是否在**第一次** init 前写入 |
| Adapter 红灯 | adapter 与网络 SDK 版本不匹配（Debugger 会标） |
| 包体暴涨 | 一次加太多网络；先 Meta / Unity / Pangle / Mintegral 等再扩 |

下一篇：[iOS 集成加深](ios.md) · [加网络与 Bidding](networks-bidding.md) · 返回 [MAX 概览](index.md)
