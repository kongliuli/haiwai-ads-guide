# Meta AN · 广告格式

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Ad formats](https://developers.facebook.com/documentation/audience-network/ad-formats) · 广告设置 [Android](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/android) / [iOS](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/ios) / [Unity](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/unity)

生产路径请经 [聚合 Bidding](via-mediation.md)：在 Monetization Manager 建 **Placement** 时选对格式，再映射到主聚合广告单元。下列要点来自官方「广告格式」页，用于选型与合规展示；直连 SDK 的代码细节以官方 Ad Setup 为准。

## 格式速查

| 格式 | 典型场景 | 经聚合时注意 |
|------|----------|--------------|
| 横幅 Banner | 页顶/页底常驻 | 自适应横幅高度过大时，Meta 侧有时需用 **中矩形** Placement |
| 中矩形 Medium Rectangle | 约 300×250 内容区 | 可与横幅同类规范；控制台可从横幅改版位 |
| 插屏 Interstitial | 关卡/流程自然断点 | 勿在启动、退出、操作中途强弹 |
| 原生 Native | 信息流混排 | 必须标「广告/赞助」+ AdChoices；素材渲染有硬性要求 |
| 原生横幅 Native Banner | 窄条原生 | 同上；无完整媒体区时常用此格式 |
| 激励视频 Rewarded Video | 用户主动看完领奖 | 先说清奖励；勿强迫；另见 [政策](guidelines.md) 激励专条 |
| 激励插屏 Rewarded Interstitial | 断点可选奖励 | 映射时有的聚合选「Rewarded」单元填激励插屏 Placement ID |

## 横幅与中矩形

- 不要盖在文字、图片、其它可点击控件上，减少误点。  
- 每页（或用户滚动时）尽量只展示**一条**广告。  
- 勿放在打断应用自然流程的位置。  
- **未经 Meta 书面批准，不得编辑/修改**横幅或中矩形创意。

官方实现：[Android Banner](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/android/banner) · [iOS Banner](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/ios/banner)

## 插屏

- 插在体验的**自然停顿**（如关卡之间），不要放在加载页、退出页或游戏进行中。  
- CTA 应以让用户**刻意点击**的方式呈现。  
- 未经书面批准不得编辑/修改插屏创意。

官方实现：[Android Interstitial](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/android/interstitial) · [iOS Interstitial](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/ios/interstitial)

## 原生

要点（违反易导致无效展示或政策问题）：

- 明确标记为「赞助内容 / 推广内容 / 广告」，并加入可展开的 **AdOptions / AdChoices**（iOS `FBAdOptionsVideo` · Android `AdOptionsVideo`）。  
- 展示广告主创意；可缩放图片，但**勿遮挡、覆盖、扭曲或改素材**。  
- 系列图比例建议约 **1.91:1～1:1**；图标/头像保持正方形。  
- 广告主名称至少留约 20 字符展示空间，超出用省略号。  
- **必须**含标题与 CTA；CTA 全文展示、勿改写；CTA 最长约 25 字符。  
- 若广告主提供评分、库存等元数据，应一并展示。

官方实现：[Android Native](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/android/native) · [iOS Native](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/ios/native)

## 原生横幅

- 同样标明「赞助 / 推广 / 广告」+ 可展开 AdOptionsView。  
- 未经批准不得改广告主创意。

官方：[Android Native Banner](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/android/native-banner) · [iOS Native Banner](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/ios/native-banner)

## 激励视频

- 放在自然休息点（关卡间、会话结束等）。  
- **展示前**向用户说清奖励；不要打断游戏或强迫观看。  
- 未经批准不得修改激励视频创意。  
- 完整激励政策（主动选择、禁止现金奖励等）见 [guidelines.md](guidelines.md)。

官方：[Android Rewarded Video](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/android/rewarded-video) · [iOS Rewarded Video](https://developers.facebook.com/documentation/audience-network/guides/setting-up/ad-setup/ios/rewarded-video)

## 激励插屏

- 放在自然转换点（如关卡之间）。  
- 不要破坏体验或出现在意外时机。  
- 未经批准不得修改创意。

官方：[Android Rewarded Interstitial](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/android/rewarded-interstitial) · [iOS Rewarded Interstitial](https://developers.facebook.com/documentation/audience-network/setting-up/ad-setup/ios/rewarded-interstitial)

## 相关页

- [概览](index.md) · [经聚合 Bidding](via-mediation.md) · [政策与规范](guidelines.md) · [栏目地图](portal-map.md)
