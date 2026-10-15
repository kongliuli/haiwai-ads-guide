# AdMob 官方文档平台 · 栏目地图

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[AdMob for Developers](https://developers.google.com/admob)（文档站顶部可切换 Android / iOS / Unity / Flutter）

本页把 Google 官方 AdMob 开发者站的**栏目树**映射到本中文站：每行给出官方入口，并标注本站已有链接或「待写」。状态随批次更新；版本号与 API 名以官网为准。

总览入口：[AdMob 概览](index.md) · 全站选题表：[catalog.md](../../catalog.md)

---

## 平台切换说明

官方几乎所有 SDK 页都带平台选择器：`Android` · `iOS` · `Unity` · `Flutter`（以及部分页的 Android Legacy / Next-Gen）。  
本站以 **Android / iOS 原生** 为主干，**Unity / Flutter** 见专页；Mediation、隐私、测试等横切主题两端共用概念。

| 平台 | 官方起步 | 本站 |
|------|----------|------|
| Android | [Quick start](https://developers.google.com/admob/android/quick-start) | [android-getting-started](android-getting-started.md) |
| iOS | [Quick start](https://developers.google.com/admob/ios/quick-start) | [ios-getting-started](ios-getting-started.md) |
| Unity | [Get started](https://developers.google.com/admob/unity/quick-start) | [unity-flutter](unity-flutter.md) |
| Flutter | [Get started](https://developers.google.com/admob/flutter/quick-start) | [unity-flutter](unity-flutter.md) |

---

## 1. 产品与账号（跨平台）

| 栏目 | 官方 | 本站 |
|------|------|------|
| AdMob 产品介绍 | https://developers.google.com/admob | [index.md](index.md) |
| 控制台 / 应用与广告单元 | https://admob.google.com/ | [index.md](index.md)（概览） |
| 结算与付款 | Support / Payments（控制台内） | [ops/payout](../../ops/payout.md) |
| AdMob API（REST 拉报表等） | https://developers.google.com/admob/api/v1/getting-started | 待写 |

---

## 2. 接入起步（按平台）

| 栏目 | Android 官方 | iOS 官方 | 本站 |
|------|--------------|----------|------|
| SDK 快速接入 | [quick-start](https://developers.google.com/admob/android/quick-start) | [quick-start](https://developers.google.com/admob/ios/quick-start) | [Android](android-getting-started.md) · [iOS](ios-getting-started.md) |
| SDK 下载 / 版本 | [download](https://developers.google.com/admob/android/download) | [download](https://developers.google.com/admob/ios/download) | 见各起步页 |
| 发布前检查清单 | [release](https://developers.google.com/admob/android/release-checklist) 等 | 同左 iOS 树 | 待写 |
| Unity 插件接入 | — | — | [unity-flutter](unity-flutter.md) |
| Flutter 插件接入 | — | — | [unity-flutter](unity-flutter.md) |

---

## 3. 广告格式

两端栏目对称；官方路径形如 `/admob/{android|ios}/{format}`。选型与要点见本站汇总页。

| 格式 | Android | iOS | 本站 |
|------|---------|-----|------|
| 总览 / 选型 | （各格式页） | （各格式页） | [formats.md](formats.md) |
| Banner | [banner](https://developers.google.com/admob/android/banner) | [banner](https://developers.google.com/admob/ios/banner) | [formats.md](formats.md)#横幅banner |
| Interstitial | [interstitial](https://developers.google.com/admob/android/interstitial) | [interstitial](https://developers.google.com/admob/ios/interstitial) | [formats.md](formats.md) |
| Rewarded | [rewarded](https://developers.google.com/admob/android/rewarded) | [rewarded](https://developers.google.com/admob/ios/rewarded) | [formats.md](formats.md) |
| Rewarded interstitial | [rewarded-interstitial](https://developers.google.com/admob/android/rewarded-interstitial) | 同左 | [formats.md](formats.md) |
| App open | [app-open](https://developers.google.com/admob/android/app-open) | 同左 | [formats.md](formats.md) |
| Native | [native](https://developers.google.com/admob/android/native) | 同左 | [formats.md](formats.md) |
| Unity / Flutter 各格式 | `/admob/unity/...` · `/admob/flutter/...` | — | [unity-flutter](unity-flutter.md)（入口）；单格式深页 待写 |

---

## 4. 测试与调试

| 栏目 | Android | iOS | 本站 |
|------|---------|-----|------|
| Test ads（测试单元 / 测试设备） | [test-ads](https://developers.google.com/admob/android/test-ads) | [test-ads](https://developers.google.com/admob/ios/test-ads) | [testing.md](testing.md) |
| 调试日志 / Inspector 等 | 见 test-ads 与 Mediation 调试小节 | 同左 | [testing.md](testing.md) |
| Unity / Flutter 测试 | `/admob/unity/test-ads` 等 | — | [testing.md](testing.md) · [unity-flutter](unity-flutter.md) |

---

## 5. 隐私 / UMP / 同意

| 栏目 | Android | iOS | 本站 |
|------|---------|-----|------|
| UMP SDK 接入 | [privacy](https://developers.google.com/admob/android/privacy) | [privacy](https://developers.google.com/admob/ios/privacy) | [privacy-ump.md](privacy-ump.md) · 工程清单 [ops/privacy](../../ops/privacy.md) |
| GDPR / EEA 披露 | Support + privacy/gdpr 子页 | [gdpr](https://developers.google.com/admob/ios/privacy/gdpr) 等 | 同上 |
| iOS ATT / IDFA 消息 | — | Privacy & messaging + ATT | [privacy-ump.md](privacy-ump.md) · [ops/privacy](../../ops/privacy.md) |
| 儿童 / 年龄限制流量 | TFCD / TFUA 等文档 | 同左 | [ops/privacy](../../ops/privacy.md)（清单）；深页可并入 privacy-ump |
| Unity / Flutter UMP | `/admob/unity/privacy` · `/admob/flutter/privacy` | — | [privacy-ump.md](privacy-ump.md)（要点） |

---

## 6. Mediation（聚合）

| 栏目 | Android | iOS | 本站 |
|------|---------|-----|------|
| Mediation 起步 | [mediation](https://developers.google.com/admob/android/mediation) | [mediation](https://developers.google.com/admob/ios/mediation) | [mediation.md](mediation.md) · 总论 [mediation/overview](../../mediation/overview.md) |
| 各广告源 Adapter 页 | mediation 下列表（Meta、Unity…） | 同左 | [mediation.md](mediation.md)；单源深页 待写 |
| Bidding vs Waterfall | 文档与控制台说明 | 同左 | [mediation.md](mediation.md) |
| Unity / Flutter Mediation | `/admob/unity/mediation` 等 | — | 待写（入口见 [unity-flutter](unity-flutter.md)） |

---

## 7. 其它常见栏目（本站进度）

| 栏目 | 官方入口示例 | 本站 |
|------|--------------|------|
| 政策与违规（无效流量等） | AdMob Help / Program policies | 待写（可链 Support） |
| 报表与指标解读 | 控制台 Reports | 待写 |
| 自定义事件 / 自有网络 | Custom events（mediation 子树） | 待写 |
| GMA Next-Gen SDK 迁移 | Android Next-Gen 文档树 | 待写（起步页已点到坐标变化） |

---

## 怎么用这张地图

1. 先按你的技术栈打开对应官方起步页，对照本站中文步骤。  
2. 格式、测试、隐私、Mediation 走本站深页；遇版本差异点回「对照原文」。  
3. 标「待写」的栏目可开 Issue / 下一批补文；勿把官网整页 verbatim 贴进仓库。
