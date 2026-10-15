# Unity LevelPlay · 官方文档平台地图

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Unity LevelPlay](https://docs.unity.com/en-us/grow/levelplay) · [Platform](https://docs.unity.com/en-us/grow/levelplay/platform) · [SDK](https://docs.unity.com/en-us/grow/levelplay/sdk) · [Account](https://docs.unity.com/en-us/grow/levelplay/account)

Unity Grow Docs 把 LevelPlay 分成三大块：**Platform**（控制台与变现配置）、**SDK**（Unity / Android / iOS 集成）、**Account**（账号与权限）。本页是栏目对照表；中文步骤见右侧「本站」列。

状态：`已写` / `待写`（官方有、本站尚未单独成篇）。

---

## Platform（控制台）

官方入口：[LevelPlay Platform](https://docs.unity.com/en-us/grow/levelplay/platform)

| 官方栏目 | 官方入口 | 本站 | 状态 |
|----------|----------|------|------|
| Get started | [get-started](https://docs.unity.com/en-us/grow/levelplay/platform/get-started) | [platform-basics](platform-basics.md) · [testing](testing.md) · [index](index.md) | 已写（摘要） |
| Fundamentals | [fundamentals](https://docs.unity.com/en-us/grow/levelplay/platform/fundamentals) | [mediation-networks](mediation-networks.md) · [platform-basics](platform-basics.md) | 已写（网络/广告位） |
| Reporting / Measurement | [measurement](https://docs.unity.com/en-us/grow/levelplay/platform/measurement) | [reporting](reporting.md) | 已写 |
| Advanced settings | [settings/advanced](https://docs.unity.com/en-us/grow/levelplay/platform/settings/advanced) | [platform-basics](platform-basics.md)（placements / capping 等） | 已写（要点） |
| APIs | [platform/api](https://docs.unity.com/en-us/grow/levelplay/platform/api) | — | 待写 |
| Best practices | [best-practices](https://docs.unity.com/en-us/grow/levelplay/platform/best-practices) | — | 待写 |
| Legal | Platform 栏目下 Legal resources | — | 待写（以官网为准） |

### Get started 子题（对照）

| 官方主题 | 典型原文 | 本站 |
|----------|----------|------|
| 介绍 / Welcome kit / 注册账号 | [start](https://docs.unity.com/en-us/grow/levelplay/platform/get-started/start) | [index](index.md) |
| 添加应用 | 官网 Add an app（Dashboard → New App） | [platform-basics](platform-basics.md) |
| 管理广告位（Ad units） | [ad-units](https://docs.unity.com/en-us/grow/levelplay/platform/get-started/ad-units) | [platform-basics](platform-basics.md) |
| Mediation networks / Instances | Get started 子页 | [mediation-networks](mediation-networks.md) |
| Integration testing | [integration-testing](https://docs.unity.com/en-us/grow/levelplay/platform/get-started/integration-testing) | [testing](testing.md) |

### Fundamentals 子题（对照）

含 Mediated networks、Mediation management、Instance rate、In-app bidding、A/B test、Impression-level revenue 等。个人开发者优先读：网络与 Bidding 概念 → [mediation-networks](mediation-networks.md)；ILR / A/B 等深页待写。

### Reporting 子题（对照）

| 官方主题 | 原文 | 本站 |
|----------|------|------|
| Home / Real-time pivot / Performance / Cohorts | [measurement](https://docs.unity.com/en-us/grow/levelplay/platform/measurement) | [reporting](reporting.md) |
| Schedule custom reports | [schedule](https://docs.unity.com/en-us/grow/levelplay/platform/measurement/schedule) | 同上 |
| Activity logs | measurement 栏目 | 同上（一笔带过） |

### Advanced / APIs / Best practices

- **Advanced**：Placements、Segments、Direct deals、Capping & pacing、Rewarded / S2S callback → 本站在 [platform-basics](platform-basics.md) 给个人向要点；完整字段以官网为准。  
- **APIs**：鉴权、Reporting API、Application / Ad Units / Groups / Instances / Placements API → 本站暂不写实现，个人极少需要。  
- **Best practices**：延迟、Bidding、Placements、A/B、Segments → 待写。

---

## SDK（客户端）

官方入口：[LevelPlay SDK](https://docs.unity.com/en-us/grow/levelplay/sdk)

各引擎侧通常都有：Get started → Regulations → Ad formats → Mediated Networks → Test your integration。

| 引擎 | 官方入口 | 本站 | 状态 |
|------|----------|------|------|
| Unity | [sdk/unity](https://docs.unity.com/en-us/grow/levelplay/sdk/unity) | [unity-package](unity-package.md) · [mediation-networks](mediation-networks.md) · [testing](testing.md) | 已写 |
| Android | [sdk/android](https://docs.unity.com/en-us/grow/levelplay/sdk/android) | [android-native](android-native.md) · [testing](testing.md) | 已写 |
| iOS | [sdk/ios](https://docs.unity.com/en-us/grow/levelplay/sdk/ios) | —（Unity 工程走 Unity 包；纯原生 iOS 待写） | 待写 |

常用原文直达：

| 主题 | Unity | Android |
|------|-------|---------|
| Package / SDK 集成 | [package-integration](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/package-integration) | [sdk-integration](https://docs.unity.com/en-us/grow/levelplay/sdk/android/sdk-integration) |
| Mediation Networks | [mediation-networks](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/mediation-networks) | 各网络 Android guides |
| Integration Helper | [integration-helper](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/integration-helper) | [integration-helper](https://docs.unity.com/en-us/grow/levelplay/sdk/android/integration-helper) |

---

## Account（账号）

官方入口：[Account](https://docs.unity.com/en-us/grow/levelplay/account)

| 官方主题 | 说明 | 本站 | 状态 |
|----------|------|------|------|
| User management | 添加/移除团队成员、权限 | [index](index.md)（结算/账号一笔） | 待写（深页） |
| Account user profiles | 角色与资源访问级别 | — | 待写 |

个人开发者：先用 [Unity Dashboard](https://dashboard.unity3d.com/) 完成变现开通与应用创建即可；多人协作再回官网 Account 章节。

---

## 本站阅读顺序（个人）

1. [概览](index.md) → [platform-basics](platform-basics.md)（控制台建应用 / 广告位）  
2. 引擎：[unity-package](unity-package.md) 或 [android-native](android-native.md)  
3. [testing](testing.md) 验证 → [mediation-networks](mediation-networks.md) 加网络  
4. 上线后看 [reporting](reporting.md)

总入口：[portals.md](../../portals.md) · [catalog.md](../../catalog.md)
