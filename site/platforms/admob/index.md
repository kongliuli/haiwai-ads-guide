# Google AdMob · 概览与账号

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[AdMob for Developers](https://developers.google.com/admob) · 控制台 [admob.google.com](https://admob.google.com/)

**栏目与进度**：[官方平台栏目地图](portal-map.md) · [测试与调试](testing.md) · [隐私与 UMP](privacy-ump.md) · [Unity / Flutter](unity-flutter.md)

## 这是什么

AdMob 是 Google 面向移动应用的广告变现平台：你在 App 里留广告位，Google 匹配广告主，按展示/点击等结算收益。个人开发者可直接用 Individual 身份注册，是出海 App 最常见的第一站。

## 你需要准备

- 可上架的 Android 和/或 iOS 应用（公开商店链接；私有 Play 应用通常无法绑定）  
- Google 账号；按提示完成支付资料与地址验证（常见 PIN 码邮件）  
- 了解目标地区的隐私要求（EEA 同意、iOS ATT 等）

## 推荐路径

1. 打开控制台创建应用，拿到 **App ID**（形如 `ca-app-pub-xxxx~yyyy`）  
2. 按平台接入 Google Mobile Ads SDK → [Android](android-getting-started.md) / [iOS](ios-getting-started.md) / [Unity·Flutter](unity-flutter.md)  
3. 创建广告单元，先用**官方测试广告单元**验证（见 [测试](testing.md)），再换正式 ID；隐私地区接 [UMP](privacy-ump.md)  
4. 日活上来后，在 AdMob 后台开 **Mediation**，挂 Meta / Unity 等源（见 [聚合](../../mediation/overview.md)）

## 结算速记

常见电汇、Payoneer 等；门槛多与 AdSense 共用支付资料，起付线常见 **$100**（以控制台 Payments 为准）。

## 本地 SDK 材料

仓库内归档见 `materials/sdk/admob/`（iOS zip、Android AAR 等）。
