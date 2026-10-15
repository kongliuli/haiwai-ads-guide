# AdMob · 广告格式选型与接入要点

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文（Android）：[Banner](https://developers.google.com/admob/android/banner) · [Interstitial](https://developers.google.com/admob/android/interstitial) · [Rewarded](https://developers.google.com/admob/android/rewarded) · [Rewarded interstitial](https://developers.google.com/admob/android/rewarded-interstitial) · [App open](https://developers.google.com/admob/android/app-open) · [Native](https://developers.google.com/admob/android/native)  
> 对照原文（iOS）：[Banner](https://developers.google.com/admob/ios/banner) · [Interstitial](https://developers.google.com/admob/ios/interstitial) · [Rewarded](https://developers.google.com/admob/ios/rewarded) · [Rewarded interstitial](https://developers.google.com/admob/ios/rewarded-interstitial) · [App open](https://developers.google.com/admob/ios/app-open) · [Native](https://developers.google.com/admob/ios/native)

先完成 [Android](android-getting-started.md) / [iOS](ios-getting-started.md) SDK 初始化与 App ID，再按格式建广告单元。两端 API 名称不同，流程一样：**建单元 → 用测试 ID 验通路 → load → 在合适时机 show / 绑定视图 → 换正式 ID**。

## 测试广告单元（必读）

开发阶段只用 Google 提供的**测试广告单元 ID**，不要拿正式单元在真机上狂刷。

- 官方维护一份各格式测试 ID 列表，随 SDK 文档更新：  
  - Android：[Test ads](https://developers.google.com/admob/android/test-ads)  
  - iOS：[Test ads](https://developers.google.com/admob/ios/test-ads)  
- 也可在正式单元上加**测试设备**（AdMob 控制台或代码注册 test device），上架前务必关掉。  
- 未上架应用、未关联商店链接时用正式单元刷量，有账号风险。

## 格式怎么选（个人开发者速查）

| 格式 | 适合场景 | 体验风险 | 常见收益感 |
|------|----------|----------|------------|
| 横幅 Banner | 工具页底部/顶部常驻 | 低（别挡主操作） | 稳但偏低 |
| 插屏 Interstitial | 关卡结束、流程自然断点 | 高（频次要控） | 中高 |
| 激励视频 Rewarded | 换金币、额外机会、去广告时段 | 低（用户主动） | 通常最高 |
| 激励插屏 Rewarded interstitial | 想要插屏位但给可选奖励 | 中 | 介于插屏与激励之间 |
| 开屏 App open | 冷启动 / 从后台回前台 | 中（别连环弹） | 中 |
| 原生 Native | 信息流、列表混排 | 中（要自己排版合规） | 看创意与布局 |

**建议起步组合**：工具类 → Banner + 偶发插屏；内容/游戏 → Rewarded 为主，辅以插屏；再考虑开屏。原生等你有设计师或成熟信息流再上。

## 横幅（Banner）

- **控制台**：创建 Banner 广告单元，记下 Unit ID。  
- **Android**：用 `AdView` / 锚定自适应横幅（Adaptive Banner）放入布局；`loadAd` 前设好 Unit ID 与尺寸。见 [Android Banner](https://developers.google.com/admob/android/banner)。  
- **iOS**：用 `GADBannerView`（或当前文档推荐的 Banner API），设 `adUnitID`、`rootViewController`，再 `load`。见 [iOS Banner](https://developers.google.com/admob/ios/banner)。  
- **要点**：优先自适应宽度；避免叠在可点击主按钮上；页面销毁时释放视图，防泄漏。

## 插屏（Interstitial）

- 全屏、适合「用户刚完成一段任务」的空隙，**不要**在启动瞬间或连点操作中弹出。  
- 流程：预加载 → 在断点检查 `isLoaded` / 就绪回调 → `show` → 关闭后再预加载下一条。  
- 官方页：[Android](https://developers.google.com/admob/android/interstitial) · [iOS](https://developers.google.com/admob/ios/interstitial)。  
- **频次**：个人 App 宁可少弹；可用会话计数 / 冷却时间自管，别依赖「能弹就弹」。

## 激励视频（Rewarded）

- 用户点「看广告领奖励」再展示；**务必在发放奖励的回调里发奖**，并做防重复发放。  
- 预加载策略与插屏类似；失败时给用户明确提示（「暂无广告，稍后再试」），不要空转。  
- 官方页：[Android](https://developers.google.com/admob/android/rewarded) · [iOS](https://developers.google.com/admob/ios/rewarded)。  
- 变现向产品优先把激励位做稳，再开 [Mediation](mediation.md) 抬 eCPM。

## 激励插屏（Rewarded interstitial）

- 外观接近插屏，但可在展示前告知「看完可领奖」；适合不想单独做按钮、又想给补偿的关卡间隙。  
- 接入面与激励类似（独立广告单元与 API）。  
- 官方页：[Android](https://developers.google.com/admob/android/rewarded-interstitial) · [iOS](https://developers.google.com/admob/ios/rewarded-interstitial)。  
- 与普通插屏**不要**在同一断点叠着弹。

## 开屏（App open）

- 在冷启动或热启动回到前台时展示；加载有超时概念，超时就进主页，别卡死启动。  
- 控制：**冷启动最多一次**、从广告页回前台不要立刻再弹、与插屏错开。  
- 官方页：[Android](https://developers.google.com/admob/android/app-open) · [iOS](https://developers.google.com/admob/ios/app-open)。

## 原生（Native）

- 素材（图、标题、CTA 等）由你排进自己的 UI；必须按政策展示广告标识与可关闭/可点击区域。  
- 工作量大，适合信息流 App；小工具优先 Banner / 激励。  
- 官方页：[Android](https://developers.google.com/admob/android/native) · [iOS](https://developers.google.com/admob/ios/native)。  
- 布局改版后重新走政策自查，避免「伪装系统通知」类违规。

## 接入检查清单（各格式通用）

1. Manifest / Info.plist 里 App ID 正确，且已 `MobileAds` / 等价初始化。  
2. 测试 ID 能展示；再换控制台正式 Unit ID。  
3. 监听加载失败与展示失败，失败时降级到无广告体验，不要崩。  
4. iOS 注意 ATT / UMP；EEA 等地区同意后再请求个性化广告（见 [隐私占位](../../ops/privacy.md)）。  
5. 日活上来后同一格式可进 [AdMob Mediation](mediation.md)，让多家源竞价。

相关：[AdMob 概览](index.md) · [聚合总论](../../mediation/overview.md)
