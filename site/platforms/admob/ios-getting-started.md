# AdMob · iOS 接入起步

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[iOS quick start](https://developers.google.com/admob/ios/quick-start) · [SDK 下载](https://developers.google.com/admob/ios/download)

## 1. 工程前提

- 满足官网当前 Xcode / 最低 iOS 版本要求  
- AdMob 控制台已创建 iOS 应用，拿到 **App ID**

## 2. 安装 SDK（三选一）

**推荐 CocoaPods**

```ruby
pod 'Google-Mobile-Ads-SDK'
```

也可使用 Swift Package Manager，或从下载页获取 `googlemobileadssdkios.zip` 手动拖入。

手动集成时通常需嵌入：

- `GoogleMobileAds.xcframework`  
- `UserMessagingPlatform.xcframework`  

并按文档设置 Embed & Sign、`-ObjC` 等链接选项。

## 3. Info.plist

写入 AdMob App ID（键名以当前文档为准，常见为 `GADApplicationIdentifier`），并按需配置 `SKAdNetworkItems`、ATT 相关说明文案。

## 4. 初始化与测试

在合适生命周期调用启动 API，先加载**测试广告单元**，确认展示与回调正常后再换正式 ID。

## 5. 隐私

面向欧盟等地区需接入用户消息平台（UMP）征求同意；iOS 14+ 需处理 ATT。细节见后续 [隐私占位](../../ops/privacy.md)。

返回：[AdMob 概览](index.md) · [Android 起步](android-getting-started.md)
