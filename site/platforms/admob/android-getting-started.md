# AdMob · Android 接入起步

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Set up Google Mobile Ads SDK (Legacy)](https://developers.google.com/admob/android/quick-start) · 下载说明 [Android download](https://developers.google.com/admob/android/download)  
> 版本参考：文档常见 `play-services-ads:25.5.0`（以官网为准）

## 1. 工程前提

- 使用较新的 Android Gradle Plugin；`minSdk` / `compileSdk` 以满足官方当前要求为准（Legacy 文档常要求较高 compileSdk）  
- 在 AdMob 控制台创建应用，复制 **App ID**

## 2. 加依赖

`settings.gradle` / 根仓库已含 Google Maven 时，在 app 模块：

```groovy
dependencies {
  implementation("com.google.android.gms:play-services-ads:25.5.0")
}
```

（若你跟随官网迁到 GMA Next-Gen SDK，坐标会变为 `com.google.android.libraries.ads.mobile.sdk:ads-mobile-sdk`——以官网迁移页为准。）

## 3. 写入 App ID

在 `AndroidManifest.xml` 的 `<application>` 内：

```xml
<meta-data
  android:name="com.google.android.gms.ads.APPLICATION_ID"
  android:value="ca-app-pub-xxxxxxxx~yyyyyyyy"/>
```

测试阶段可用官方示例 App ID；上架前换成自己的。

## 4. 初始化

在展示广告前调用 `MobileAds.initialize(...)`（具体 API 以当前 SDK 文档为准；Next-Gen 要求在后台线程初始化）。初始化完成后再 `load` 广告。

## 5. 验证

- 使用官方**测试广告单元 ID**，确认能拉到测试创意  
- 打开 Logcat 看适配器初始化是否成功  
- 正式广告单元绑到已上架应用后再放量

## 常见坑

- Manifest 漏写 App ID → 初始化失败或崩溃提示  
- 用正式广告单元在未上架/未关联应用上狂刷 → 账号风险  
- 只接 AdMob 网络、忽略 Mediation → 后期 eCPM 天花板偏低  

下一篇：[iOS 起步](ios-getting-started.md) · 返回 [AdMob 概览](index.md)
