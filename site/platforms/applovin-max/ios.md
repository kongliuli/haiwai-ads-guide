# AppLovin MAX · iOS 集成加深

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[iOS Integration](https://support.applovin.com/en/max/ios/overview/integration) · [Test mode](https://support.applovin.com/en/max/ios/testing-networks/test-mode) · [Mediation Debugger](https://support.applovin.com/en/max/ios/testing-networks/mediation-debugger) · [Preparing mediated networks](https://support.applovin.com/en/max/ios/preparing-mediated-networks)  
> 本地材料：[materials/sdk/applovin-max/SOURCE.md](../../../materials/sdk/applovin-max/SOURCE.md)

与 Android 同序：**装 SDK → SDK Key → 启动时初始化 → 测试模式**，再开 [Mediation / Bidding](networks-bidding.md)。

## 1. 工程前提

- 最低部署目标 **iOS 12.0+**  
- **Xcode 15+**（以官网当前页为准）  
- 含 Swift 制品时：Build Settings → Always Embed Swift Standard Libraries = **YES**；若仍支持很老的 12.2 及以下，按文档把 `/usr/lib/swift` 加到 Runpath Search Paths  
- 控制台已建 iOS 应用与广告位；**SDK Key** 在 Account → General → Keys  

发布更新可关注 [AppLovin-MAX-SDK-iOS](https://github.com/AppLovin/AppLovin-MAX-SDK-iOS)。本仓库有源码型快照 `AppLovin-MAX-SDK-iOS-master.zip`，**生产仍建议 CocoaPods / SPM**。

## 2. 安装 SDK（二选一）

### CocoaPods（常用）

```ruby
pod 'AppLovinSDK'
```

```bash
pod install --repo-update
```

### Swift Package Manager

Xcode → File → Add Package Dependencies…，填入官方 SPM 仓库 URL（见 Integration 页链接），Dependency Rule 选好后把 `AppLovinSDK` 加到 App Target。

手动 xcframework 路径见 Support Center「manual」说明；个人项目优先 Pod/SPM，少踩 Embed & Sign 坑。

### （可选）Ad Review

登录 AppLovin 账号，下载 `AppLovinQualityServiceSetup-ios.rb` 放到工程目录后执行 `ruby AppLovinQualityServiceSetup-ios.rb`。步骤以官网为准。

## 3. SDK Key

主路径：在 `ALSdkInitializationConfiguration` 里传入（App Delegate 启动时创建）：

```swift
let initConfig = ALSdkInitializationConfiguration(sdkKey: "YOUR_SDK_KEY") { builder in
  builder.mediationProvider = ALMediationProviderMAX
}
```

Key 位置同 Android：Account → General → Keys。部分隐私相关 URI 也可写在 Info.plist（见官网 Example）。

## 4. 初始化（启动时）

在 `application(_:didFinishLaunchingWithOptions:)` 尽早初始化：

```swift
ALSdk.shared().initialize(with: initConfig) { _ in
  // 完成后再 load 广告
}
```

Objective-C 对应 `[[ALSdk shared] initializeWithConfiguration:completionHandler:]`。尽早 init 是为了给 mediated 网络缓存时间。

可选（按需）：

- `settings.userIdentifier`  
- Terms & Privacy Policy Flow（隐私政策 / ToS URL；也可放 Info.plist）  
- ATT：iOS 14+ 必须按 [Privacy](https://support.applovin.com/en/max/ios/overview/privacy) 与本站 [隐私占位](../../ops/privacy.md) 处理  
- SKAdNetwork：按 [SKAdNetwork](https://support.applovin.com/en/max/ios/overview/skadnetwork) 把各网络 ID 写入 Info.plist（加 Bidding 网络后清单会变长）

## 5. 测试模式与 Mediation Debugger

测试广告不计费、不计收入。

### 代码打开

首次创建配置时写入本机 **IDFA**（ATT 拒绝时 IDFA 可能全零，需结合 Debugger / 真机授权排查）：

```swift
let initConfig = ALSdkInitializationConfiguration(sdkKey: "YOUR_SDK_KEY") { builder in
  builder.mediationProvider = ALMediationProviderMAX
  builder.testDeviceAdvertisingIdentifiers = ["YOUR_IDFA"]
}
```

控制台日志出现 `Test Mode On: true` 即成功。也可在 Mediation Debugger 里对某一网络点 Enable Test Ad 后**重启 App**。

### Mediation Debugger

用于核对 adapter / 网络 SDK 版本、缺 SKAdNetwork ID 等问题。Debug 构建保留入口；正式用户勿默认展示。

## 6. 接广告格式之前

1. 控制台拿到各格式 Ad Unit ID  
2. 等 initialize 完成再 load  
3. 插屏 / 激励：失败指数退避重试；关闭后立刻预加载  
4. Banner 保持在屏且可见  

格式页：Support Center → iOS → Ad formats。

## 常见坑

| 现象 | 优先检查 |
|------|----------|
| 链不上 Swift 库 | Always Embed Swift Standard Libraries |
| 无测试广告 | IDFA 是否在首次 init 写入；ATT 是否已授权 |
| SKAdNetwork 警告 | Info.plist 是否随新网络更新 |
| 中国大陆流量与 Pangle | 新版 adapter 常要求大陆走 CSJ，见 [networks-bidding](networks-bidding.md) |

下一篇：[加网络与 Bidding](networks-bidding.md) · [Android 集成加深](android.md) · 返回 [MAX 概览](index.md)
