# AppLovin MAX · Testing（Test mode · Mediation Debugger · Demo app）

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Android Test mode](https://support.applovin.com/en/max/android/testing-networks/test-mode) · [Android Mediation Debugger](https://support.applovin.com/en/max/android/testing-networks/mediation-debugger) · [iOS Test mode](https://support.applovin.com/en/max/ios/testing-networks/test-mode) · [iOS Mediation Debugger](https://support.applovin.com/en/max/ios/testing-networks/mediation-debugger) · [Unity Test mode](https://support.applovin.com/en/max/unity/testing-networks/test-mode) · [Unity Mediation Debugger](https://support.applovin.com/en/max/unity/testing-networks/mediation-debugger) · Getting started → [Step 4](https://support.applovin.com/en/max/getting-started)

上架前把「SDK + adapter + 后台 Connect/Waterfall」验通。官方工具在各平台 **SDK integration guides → Testing networks**；本页汇总个人开发者最常用的三块。

**硬规则**：测试广告**不计**展示、点击、收入——只验集成，不要拿测试流量估收益。

## 1. Test mode

提高测试期拿到填充的概率；开启后 IDE 控制台会有更详细的 MAX 日志。

### 怎么开

| 方式 | 说明 |
|------|------|
| Mediation Debugger | 在已完成集成的网络上点 **Enable** Test Ad，**重启 App** 让 mediated SDK 用测试凭证初始化 |
| 代码（推荐调试机） | 在**第一次**创建 SDK 实例 / 初始化之前写入本机广告 ID |

#### Android（GAID）

```kotlin
val initConfig = AppLovinSdkInitializationConfiguration.builder("YOUR_SDK_KEY")
  .setMediationProvider(AppLovinMediationProvider.MAX)
  .setTestDeviceAdvertisingIds(listOf("YOUR_GAID"))
  .build()
```

#### iOS（IDFA）

```swift
let initConfig = ALSdkInitializationConfiguration(sdkKey: "YOUR_SDK_KEY") { builder in
  builder.mediationProvider = ALMediationProviderMAX
  builder.testDeviceAdvertisingIdentifiers = ["YOUR_IDFA"]
}
```

ATT 拒绝时 IDFA 可能全零，需结合真机授权与 Debugger 排查。

#### Unity

须在 `InitializeSdk` **之前**：

```csharp
MaxSdk.SetTestDeviceAdvertisingIdentifiers(new string[] { "YOUR_IDFA_OR_GAID" });
MaxSdk.InitializeSdk();
```

### 是否生效

初始化日志段出现 `Test Mode On: true`。若测试广告不来：可再试 live；**无 fill 在测试期很常见**，不等于集成坏了。

平台集成页也有摘要：[android.md](android.md) §5 · [ios.md](ios.md) §5。

## 2. Mediation Debugger

SDK 内置联调面板（**不支持** Custom SDK 网络）。用来确认：adapter 是否装上、网络 SDK 与 adapter 版本是否匹配、缺 SKAdNetwork ID 等。

### 打开方式

```kotlin
// Android
AppLovinSdk.getInstance(this).showMediationDebugger()
```

```swift
// iOS
ALSdk.shared().showMediationDebugger()
```

Unity / 其他平台见官网同级 Mediation Debugger 页。Debug 包留入口即可，**正式用户勿默认弹出**。

### 四个区块（官网结构）

| 区块 | 做什么 |
|------|--------|
| **Integration status** | Completed / Incomplete / Missing；点 Incomplete 看缺什么，回 [Preparing](preparing-networks.md) 补 |
| **Testing with test ads** | 对已完成网络 Enable Test Ad → 重启 → 再进该网络打测试广告 |
| **Testing with live ads** | 按 Ad Unit 看真实 Waterfall；可单源 Load，或 Select Live Network 在自然场景强开某源（与 Test mode 互斥；部分网络视 live-on-test-device 为欺诈，优先用 test ads 验集成） |
| **Sharing** | 右上角分享，把清单发给 QA / 审稿人 |

另可在 Debugger 里核对 **app-ads.txt** 是否含 AppLovin 条目（域名须与商店 listing / Account Domain 一致）。

**建议**：Init 后等 **2–5 秒**再 Load（部分网络如 Liftoff Monetize 需要初始化时间，过早易 no-fill）。

## 3. Demo app

官方 Demo 是集成蓝图：可对照回调、广告格式示例；也可把网络 SDK 接到 Demo 里，配合 **Test mode** 看 MAX 对各格式的事件通知。

路径：各平台 **Testing networks → MAX demo app**（例如 Android / iOS / Unity 树下 `demo-app`）。提工单时官网常要求附 Demo 侧实现 + verbose 日志 + Debugger 截图。

本仓库 SDK 归档说明见 `materials/sdk/applovin-max/`（有则参考；生产仍走 Maven / Pod / Integration Manager）。

## 4. 推荐联调顺序

1. 核心 SDK init 成功，日志无红错  
2. 打开 Debugger → Completed 里应有 AppLovin；已加的 adapter 不应长期 Incomplete  
3. 开 Test mode（代码或 Debugger）→ `Test Mode On: true`  
4. 对关键 Bidding 网络打 Test Ad  
5. 后台 Connect + Ad Unit Status 打开后，再偶发用 live / 单源验证（注意欺诈误判风险）  
6. 对照 [getting-started.md](getting-started.md) Pre-launch checklist  

## 常见坑

| 现象 | 优先查 |
|------|--------|
| `Test Mode On: false` | 广告 ID 是否在**首次** init 前写入 |
| Adapter 红 / Incomplete | 版本不匹配或 Preparing 依赖漏加 |
| 有 adapter 无竞价 | Networks 未 Connect，或 Ad Unit Waterfall Status 未开 |
| Live 测被网络判异常 | 改用 Test Ad；勿在测试机长期打 live |

下一篇：[preparing-networks.md](preparing-networks.md) · [networks-bidding.md](networks-bidding.md)。返回：[getting-started.md](getting-started.md) · [portal-map.md](portal-map.md)
