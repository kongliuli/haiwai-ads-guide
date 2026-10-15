# AdMob · Mediation（聚合）怎么开

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Android Mediation](https://developers.google.com/admob/android/mediation) · [iOS Mediation](https://developers.google.com/admob/ios/mediation)

AdMob Mediation 让**同一次广告请求**按你配置的规则，在多家广告源（含 AdMob 自有网络）之间竞价或瀑布下发，通常比只接 Google 一家填充更好、eCPM 更高。概念总览也可先看 [聚合策略](../../mediation/overview.md)。

## 什么时候开

- SDK 与主广告格式（激励 / 插屏等）已经稳定，测试与正式单元都通了。  
- 有一定日活后再折腾（经验上海外 DAU 过千更值得）。  
- **只选一个主聚合层**：已用 AdMob 就走 AdMob Mediation，不要和 MAX / LevelPlay 双主聚合并行。

## 控制台侧：五步上手

1. 打开 [AdMob 控制台](https://admob.google.com/) → 中介 / Mediation。  
2. 创建 **Mediation 组**（按广告格式：激励、插屏、横幅等分开建更清晰）。  
3. 把组绑到对应 **广告单元**（或按官方指引关联应用与版位）。  
4. **添加广告源**：在「广告源」里选 Meta、Unity、AppLovin 等；按向导填各家的 App ID / Placement / Reporting 密钥。  
5. 保存后等生效；用测试设备看 Log，确认各 adapter 初始化成功、有竞价/填充日志。

各广告源还要在**对方后台**建好应用与广告位，并把凭证填回 AdMob——只开 AdMob 开关不够。

## 工程侧：加 Adapter

- 除 `play-services-ads` / `Google-Mobile-Ads-SDK` 外，按你启用的源加入对应 **Mediation Adapter** 依赖（Maven / CocoaPods / SPM 以该源的 AdMob 接入页为准）。  
- Android 总入口与源列表：[Get started with mediation](https://developers.google.com/admob/android/mediation)。  
- iOS 总入口与源列表：[Get started with mediation](https://developers.google.com/admob/ios/mediation)。  
- 点进具体网络（如 Meta）会有「在 AdMob 配置 + 在 App 加哪条依赖」两段说明，按页勾选即可。  
- Adapter 越多包体与初始化越重：先加 1～2 家你目标地区强的源，再扩。

## Bidding vs Waterfall（怎么理解）

| | Bidding（竞价） | Waterfall（瀑布） |
|--|-----------------|-------------------|
| 机制 | 多家几乎同时出价，价高者得展示 | 按你排的 eCPM / 优先级依次请求，一家不成再下一家 |
| 配置感 | 少手工排序，偏实时拍卖 | 要调序、调底价，运维重 |
| 现状 | 新接入源优先走 Bidding（如 Meta 等） | 部分源仍支持或仅支持瀑布 |
| 个人开发者建议 | **能 Bidding 就 Bidding**；少维护层级 |

实操提示：

- 同一格式的 Mediation 组里可混合，但不要指望「层级越多越好」。  
- 改完配置用**测试设备**验证；看填充率与 eCPM 再动序，避免一天改十几次。  
- 映射（广告源广告位 ↔ AdMob 单元）配错时，常见现象是某源一直 0 展示——先查 ID 是否粘贴反了。

## 验证与常见坑

- **初始化顺序**：先完成 Mobile Ads SDK 初始化，再 load；注意隐私同意（UMP）后再请求。  
- **漏加 adapter**：后台开了源、工程没依赖 → 该源永远无贡献。  
- **重复 SDK**：某游戏引擎或第三方包已带同一网络 SDK，注意版本冲突。  
- **正式/测试**：聚合联调仍优先测试广告与测试设备；过早用正式单元刷请求损账号。  
- **报表**：AdMob 中介报表与第三方后台数字会有差异（时区、归因、延迟），看趋势比盯单日绝对值有用。

## 和本站其他页的关系

- 格式怎么接：[广告格式](formats.md)  
- 先把单网络跑通：[Android 起步](android-getting-started.md) · [iOS 起步](ios-getting-started.md)  
- 选 MAX / LevelPlay 还是 AdMob 当主聚合：[聚合总论](../../mediation/overview.md)

返回：[AdMob 概览](index.md)
