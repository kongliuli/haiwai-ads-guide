# AppLovin MAX · Support Center 平台地图

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Getting started](https://support.applovin.com/en/max/getting-started) · Support Center 根路径 `support.applovin.com/en/max/`

把官方 **MONETIZE / MAX** 文档树压成一张表：左侧是 Support Center 栏目，右侧是本站中文页与进度。学接入时先跟中文页；版本号、勾选生成的 Gradle/Pod 以官网为准。

## 总览结构

| 官方顶栏 / 栏目 | 说明 | 本站 |
|-----------------|------|------|
| **Getting started** | 七步：账号 → Ad Unit → SDK/网络 → 测试 → Connect → Waterfall → 报表 | [getting-started.md](getting-started.md) |
| **SDK integration guides** | 按平台：Integration、Preparing、Testing… | 见下表 |
| **Mediated network guides** | 各 Bidding / 传统网络逐步指南 | [networks-bidding.md](networks-bidding.md) |
| **Analyze / Account**（控制台侧） | 报表、付款、Keys、Domain / app-ads.txt | 概览摘要见 [index.md](index.md)；ops 见 [ads.txt](../../ops/ads-txt.md) |

## Getting started

| 官方步骤 | 官方入口 | 本站 | 状态 |
|----------|----------|------|------|
| 七步总览 | [Getting started](https://support.applovin.com/en/max/getting-started) | [getting-started.md](getting-started.md) | 已写 |
| 账号 / 付款 / Domain | 同页 Step 1 | 同上 · [payout](../../ops/payout.md) · [ads.txt](../../ops/ads-txt.md) | 摘要 |
| 建 Ad Unit | 同页 Step 2 · 控制台 Ad Units | [getting-started.md](getting-started.md) | 已写 |
| Connect Networks / Waterfall | 同页 Step 5–6 | [networks-bidding.md](networks-bidding.md) | 已写 |
| 上线前 checklist | 同页 Pre-launch checklist | [getting-started.md](getting-started.md) · [testing.md](testing.md) | 已写 |

## SDK integration（按平台）

| 平台 | Integration | Preparing mediated networks | 本站深页 | 状态 |
|------|-------------|------------------------------|----------|------|
| Android / Amazon | [Integration](https://support.applovin.com/en/max/android/overview/integration) | [Preparing](https://support.applovin.com/en/max/android/preparing-mediated-networks) | [android.md](android.md) · [preparing-networks.md](preparing-networks.md) | 已写 |
| iOS | [Integration](https://support.applovin.com/en/max/ios/overview/integration) | [Preparing](https://support.applovin.com/en/max/ios/preparing-mediated-networks) | [ios.md](ios.md) · [preparing-networks.md](preparing-networks.md) | 已写 |
| Unity | [Integration](https://support.applovin.com/en/max/unity/overview/integration) | [Preparing](https://support.applovin.com/en/max/unity/preparing-mediated-networks) | [preparing-networks.md](preparing-networks.md)（Integration Manager） | 摘要；无独立 Unity 深页 |
| Flutter | [Integration](https://support.applovin.com/en/max/flutter/overview/integration) | 同树 Preparing | — | 待写 |
| React Native | [Integration](https://support.applovin.com/en/max/react-native/overview/integration) | 同树 Preparing | — | 待写 |

各平台还有 Overview 下的 Privacy、SKAdNetwork（iOS）、Ad formats 等；本站合规摘要见 [ops/privacy.md](../../ops/privacy.md)。

## Preparing mediated networks

| 官方页 | 本站 | 状态 |
|--------|------|------|
| [Android Preparing](https://support.applovin.com/en/max/android/preparing-mediated-networks) | [preparing-networks.md](preparing-networks.md) | 已写（要点 + 链回官网勾选生成） |
| [iOS Preparing](https://support.applovin.com/en/max/ios/preparing-mediated-networks) | 同上 | 已写 |
| [Unity Preparing](https://support.applovin.com/en/max/unity/preparing-mediated-networks) | 同上 | 已写 |
| 各网络 Connect / Placement 细则 | [networks-bidding.md](networks-bidding.md) | 已写（Meta / Unity Ads / Pangle / Mintegral 等） |

## Mediated network guides

| 官方页 | 本站 | 状态 |
|--------|------|------|
| [SDK bidder network guides](https://support.applovin.com/en/max/mediated-network-guides/sdk-bidder-network-guides) | [networks-bidding.md](networks-bidding.md) | 已写（常用四家 + 流程） |
| 单网络逐步章（Google、Meta、…） | 链回官网；本站不镜像全文 | 按需查原文 |

## Testing（Testing networks）

| 官方主题 | 典型路径（以 Android 为例；iOS / Unity 同级） | 本站 | 状态 |
|----------|-----------------------------------------------|------|------|
| Test mode | [Android](https://support.applovin.com/en/max/android/testing-networks/test-mode) · [iOS](https://support.applovin.com/en/max/ios/testing-networks/test-mode) · [Unity](https://support.applovin.com/en/max/unity/testing-networks/test-mode) | [testing.md](testing.md) | 已写 |
| Mediation Debugger | [Android](https://support.applovin.com/en/max/android/testing-networks/mediation-debugger) · [iOS](https://support.applovin.com/en/max/ios/testing-networks/mediation-debugger) · [Unity](https://support.applovin.com/en/max/unity/testing-networks/mediation-debugger) | [testing.md](testing.md) | 已写 |
| MAX Demo app | `…/testing-networks/demo-app`（各平台） | [testing.md](testing.md)（入口与用法） | 摘要 |
| Creative Debugger | 各平台 Testing networks → Creative Debugger | — | 待写 |

平台集成页里也有 Testing 摘要：[android.md](android.md) §5 · [ios.md](ios.md) §5。

## 本站文件一览

| 路径 | 对应官方栏目 |
|------|--------------|
| [index.md](index.md) | 产品/控制台入口 + 起步摘要 |
| [portal-map.md](portal-map.md) | 本页 |
| [getting-started.md](getting-started.md) | Getting started |
| [android.md](android.md) | SDK → Android Integration |
| [ios.md](ios.md) | SDK → iOS Integration |
| [preparing-networks.md](preparing-networks.md) | Preparing mediated networks |
| [networks-bidding.md](networks-bidding.md) | Mediated network guides + Connect/Waterfall |
| [testing.md](testing.md) | Testing networks（Test mode / Debugger / Demo app） |

返回：[MAX 概览](index.md) · [官方平台总表](../../portals.md) · [选题对照](../../catalog.md)
