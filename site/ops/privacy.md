# 隐私合规（工程向）

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：UMP [Android](https://developers.google.com/admob/android/privacy) / [iOS](https://developers.google.com/admob/ios/privacy) · GDPR [Disclose to EEA users](https://developers.google.com/admob/ios/privacy/gdpr) · [European regulations message](https://support.google.com/admob/answer/10113207) · [Privacy & messaging 指南](https://support.google.com/admob/answer/12226986) · Apple [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency) · [User Privacy and Data Use](https://developer.apple.com/app-store/user-privacy-and-data-use/)

本页是**工程向 checklist**，方便个人开发者对照实现；不是法律意见。EEA/UK/瑞士及各国隐私法以律师/正式合规意见为准。商店问卷（Data safety / Privacy Nutrition Labels）须与真实 SDK 行为一致。

## 概念对照（先分清）

| 缩写 | 管什么 | 典型触达 |
|------|--------|----------|
| **GDPR / EU 用户同意** | EEA、UK、瑞士等地区对广告与本地存储等的披露与同意 | Google [EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)；App 内同意弹层 |
| **UMP** | Google 的 User Messaging Platform：拉同意表单、对接 IAB TCF 等 | AdMob「Privacy & messaging」配置 + App 内 UMP SDK |
| **ATT / IDFA** | iOS 14.5+ 跟踪授权；未授权则难用 IDFA 做个性化 | 系统 ATT 弹窗；可与 UMP 的 IDFA 说明消息配合 |
| **商店披露** | Play Data safety、App Store 隐私标签 | 上架材料，与 SDK 清单对齐 |

建议顺序（Google 文档常见推荐）：**先 GDPR/UMP 同意 →（若适用且用户同意）再 ATT**。UMP 若在 AdMob 同时配置了欧洲法规消息与 IDFA 说明，可按官方「用户会看到哪些消息」自动编排。

---

## A. Google UMP（AdMob 主路径）

### 控制台

- [ ] AdMob → **Privacy & messaging** 已创建并 **Publish** 欧洲法规（GDPR / TCF）消息  
- [ ] 填好隐私政策 URL；按需配置「Do not consent」等选项  
- [ ] iOS 若用 UMP 管 ATT：另配置 IDFA 说明消息  
- [ ] 确认消息绑定到正确的 App / AdMob App ID  

### 工程

- [ ] 引入 UMP SDK 依赖（Android / iOS 分别按文档）  
- [ ] Manifest / Info.plist 中 AdMob App ID 正确  
- [ ] **每次冷启动**调用 `requestConsentInfoUpdate`（或平台等价 API）  
- [ ] 再 `loadAndShowConsentFormIfRequired`（名称以当前 SDK 为准）  
- [ ] 需要时提供可点的「Privacy and cookie settings」入口，允许用户撤回/修改同意  
- [ ] 同意完成前谨慎请求个性化广告；按文档处理 `canRequestAds` 一类门闸  
- [ ] 儿童/年龄限制流量按文档打标（如 restricted data processing），勿假设 UMP 会替你推断  

官方：

- [Set up UMP SDK · Android](https://developers.google.com/admob/android/privacy)  
- [Set up UMP SDK · iOS](https://developers.google.com/admob/ios/privacy)  
- [Disclose to EEA users](https://developers.google.com/admob/ios/privacy/gdpr)  
- [Create European regulations message](https://support.google.com/admob/answer/10113207)  

非 AdMob 主聚合时：仍可能要用**经 Google 认证的 CMP**（IAB TCF），或各网络自带的同意方案——以 MAX / LevelPlay / Meta 隐私章节为准，不要只接 SDK 却不收同意。

---

## B. iOS ATT

- [ ] `Info.plist` 配置 `NSUserTrackingUsageDescription`（文案真实、可过审）  
- [ ] 在合适时机请求 ATT（避免与无关弹窗抢焦点；常放在 GDPR 同意之后）  
- [ ] 根据授权结果设置各广告 SDK 的 tracking / 个性化开关（例如 Meta 的 `setAdvertiserTrackingEnabled`）  
- [ ] 补齐各网络要求的 **SKAdNetwork** ID 列表  
- [ ] App Store 隐私问卷与 ATT 实际行为一致  

官方：

- [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency)  
- [User Privacy and Data Use](https://developer.apple.com/app-store/user-privacy-and-data-use/)  

---

## C. GDPR / 同意逻辑（工程自检）

- [ ] EEA/UK/CH 用户能看到披露与选择，而非静默开个性化  
- [ ] 拒绝同意后：降级为非个性化或停用依赖同意的处理，且可继续基本使用（按你的产品与政策设计）  
- [ ] 用户可随时撤回；入口文案清晰（Google 指南常见要求含 Privacy and cookie settings 一类入口）  
- [ ] 聚合下的 Meta / Unity / 其他源也能读到同意信号（TCF 字符串、各 SDK 的 consent API）  
- [ ] 不在未同意时提前初始化「强依赖广告标识」的路径（按各 SDK 文档）  

政策入口：[Google EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/) · [Privacy & messaging 使用指南](https://support.google.com/admob/answer/12226986)

---

## D. 上架与多网络

- [ ] Play「数据安全」表单列出广告 SDK 收集的数据与用途  
- [ ] App Store 隐私标签与第三方 SDK 清单同步更新  
- [ ] 换聚合、加 Meta Bidding 后，**重新核对**披露与同意转发  
- [ ] 保留隐私政策页面可公网访问（UMP 消息与商店都常要求 URL）  

## 相关页

- [聚合策略](../mediation/overview.md)  
- [Meta 经聚合接入](../platforms/meta-an/via-mediation.md)  
- [ads.txt / app-ads.txt](ads-txt.md) · [结算](payout.md)
