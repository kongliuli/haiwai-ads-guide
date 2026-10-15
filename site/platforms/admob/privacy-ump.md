# AdMob · 隐私与 UMP

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[UMP · Android](https://developers.google.com/admob/android/privacy) · [UMP · iOS](https://developers.google.com/admob/ios/privacy) · [Disclose to EEA users](https://developers.google.com/admob/ios/privacy/gdpr) · Support：[European regulations message](https://support.google.com/admob/answer/10113207) · [Privacy & messaging](https://support.google.com/admob/answer/12226986)

本页讲 **AdMob 路径下** 怎么把 Google User Messaging Platform（UMP）接到产品里：控制台消息 → SDK 拉表单 → 再请求广告。  
更偏「全平台工程 checklist」（含 ATT、商店问卷、多网络）见运维篇：[隐私合规（UMP / ATT / GDPR）](../../ops/privacy.md)。  
**不是法律意见**；EEA/UK/瑞士及各国要求以正式合规意见为准。

相关：[测试与调试](testing.md) · [栏目地图](portal-map.md) · [AdMob 概览](index.md)

---

## 1. 为什么必须单独做

Google 对 EEA、英国、瑞士等地区有 **EU User Consent Policy**：涉及广告标识、本地存储等用途时，要先披露并取得同意（或按政策走合法路径），不能静默开个性化。  
UMP 是 AdMob 官方 CMP 方案：在控制台配置「Privacy & messaging」，App 内用 UMP SDK 拉取并展示同意表单，并尽量对接 IAB TCF 等信号，供 Google 与部分 Mediation 源读取。

个人开发者最小心智模型：

1. 控制台 **Publish** 好欧洲法规消息（隐私政策 URL 等填全）  
2. App 冷启动：**更新同意信息 → 必要时弹表单 → 允许后再请求广告**  
3. 提供用户日后修改同意的入口  
4. iOS 再叠加 ATT（常见顺序：先 GDPR/UMP，再 ATT）

---

## 2. 控制台：Privacy & messaging

在 [AdMob 控制台](https://admob.google.com/)：

1. 进入 **Privacy & messaging**。  
2. 创建并配置 **欧洲法规（GDPR / TCF）** 类消息：隐私政策链接、同意/拒绝选项等按向导。  
3. **Publish**，并确认绑定到正确的 AdMob 应用。  
4. iOS 若要用 UMP 编排 IDFA 说明：另配 IDFA 相关消息（与 ATT 文案、时机配合）。  
5. 改文案或选项后重新 Publish；客户端下次 `requestConsentInfoUpdate` 才会拿到新配置。

未 Publish 或绑错 App 时，真机上常见「永远不弹窗」或行为与预期不符——先回控制台核对，再查代码。

---

## 3. 工程：UMP SDK 主流程

各平台包名/API 以官网为准；逻辑相同：

```
冷启动
  → requestConsentInfoUpdate（每次都要，勿只做一次缓存死）
  → loadAndShowConsentFormIfRequired（或当前 SDK 等价 API）
  → 根据 canRequestAds / 同意状态决定是否初始化广告或 load
  → （iOS）若适用再请求 ATT
```

实践要点：

- **依赖**：按 [Android privacy](https://developers.google.com/admob/android/privacy) / [iOS privacy](https://developers.google.com/admob/ios/privacy) 加入 UMP 制品；与 GMA SDK 版本匹配。  
- **App ID**：Manifest / Info.plist 中的 AdMob App ID 必须正确，否则同意与广告链路都会怪。  
- **门闸**：在同意未完成、且文档要求不可请求广告时，不要抢先 `load` 个性化广告；跟随 `canRequestAds`（名称以 SDK 为准）。  
- **撤回**：设置页放「Privacy options」/「Privacy and cookie settings」一类入口，调用官方提供的再次展示表单 API。  
- **儿童与年龄**：TFCD / TFUA / restricted data processing 等需按应用受众单独打标；UMP 不会自动替你推断「这是儿童应用」。

Unity / Flutter：官方有对应 `privacy` 页与插件 API，语义同上——先同意，再广告。入口见 [Unity / Flutter](unity-flutter.md)。

---

## 4. 与 ATT、Mediation 的交接

| 环节 | 做什么 |
|------|--------|
| ATT | `NSUserTrackingUsageDescription` + 合适时机请求；未授权则各 SDK 走非 IDFA 路径 |
| Mediation | 选支持 TCF / 能读 Google 同意信号的源；各源若有自己的 consent API，按该源文档补设 |
| Meta 等 | 常见还需 `setAdvertiserTrackingEnabled` 等与 ATT 结果对齐（见各源文档） |
| 非 AdMob 主聚合 | MAX / LevelPlay 可能要求自带或认证 CMP——见各平台隐私章，不要假设「只接了 AdMob UMP 就覆盖一切」 |

SKAdNetwork ID 列表、App Store / Play 数据披露与真实 SDK 行为一致——细节 checklist 见 [ops/privacy.md](../../ops/privacy.md)。

---

## 5. 调试同意（开发期）

官方 privacy 文档通常提供：

- **调试地理**：把设备当成 EEA 等地区，强制走需要表单的路径。  
- **重置同意**：清掉本地同意状态，反复验首启弹窗。  
- 与 [测试广告](testing.md) 结合：用测试 Unit ID 验「同意后能出广告、拒绝后按政策降级」。

不要在生产包长期打开 debug geography。

---

## 6. 个人开发者避坑

- 只接 GMA SDK、从不弹同意 → 欧洲流量政策风险。  
- 同意与广告初始化顺序颠倒 → 竞态、难复现的 fill/个性化问题。  
- 隐私政策 URL 404 或与商店表述矛盾 → 审核与合规双杀。  
- 以为「国内不上架欧洲就永远不用 UMP」→ 用户漫游、VPN、商店地区与账号地区不一致时仍可能踩线；按产品实际分发决定，至少保留可开关的实现。

更完整的勾选清单（含商店问卷）：请直接用 [ops/privacy.md](../../ops/privacy.md)。

下一篇：[Unity / Flutter 接入](unity-flutter.md) · 返回 [AdMob 概览](index.md)
