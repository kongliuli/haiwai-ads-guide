# LevelPlay · 控制台、广告位与应用配置

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Get started](https://docs.unity.com/en-us/grow/levelplay/platform/get-started) · [Manage ad units](https://docs.unity.com/en-us/grow/levelplay/platform/get-started/ad-units) · [Advanced settings](https://docs.unity.com/en-us/grow/levelplay/platform/settings/advanced) · Dashboard [dashboard.unity3d.com](https://dashboard.unity3d.com/)

面向个人开发者：在 **LevelPlay / Unity Dashboard** 里把应用、广告单元（Ad units）和基础变现开关配好，再去接 SDK。客户端安装见 [unity-package](unity-package.md) / [android-native](android-native.md)。

## 1. 账号与入口

1. 用 Unity ID 登录 [Dashboard](https://dashboard.unity3d.com/)  
2. 开通 / 进入 **LevelPlay（Monetize / Mediation）** 相关工作区  
3. 公司信息、税务、收款等按后台提示补齐（结算见 [ops/payout](../../ops/payout.md)）

个人账号一般一人即可；需要同事看报表时，再按官网 [Account · User management](https://docs.unity.com/en-us/grow/levelplay/account) 加用户。

## 2. 添加应用

在控制台 **New App**（或 Apps → 新建）：

| 情况 | 做法 |
|------|------|
| 已上架 App Store / Google Play | 填商店 URL → **Import App Info**，核对名称与品类 |
| 尚未上架 | 用临时应用名创建；上架后在 Apps 页更新信息 |

可选：**Duplicate setup from another application**，复制 COPPA/CCPA、广告单元、Placement、capping 等，适合同系列多包名。

添加时勾选要用的广告格式（常见：Rewarded、Interstitial、Banner）。记下 **App Key**——SDK `Init` 必用。

Apps 列表常见字段（示意）：

- **Status**：Live / Temp（未进商店）  
- **Active Ad units**：正在变现的广告单元  
- **S2S rewarded callbacks**：激励服务端回调开关  

隐藏应用只是从部分配置页挪走，**仍可能继续出广告并出现在报表**，勿当成下架。

## 3. 管理广告单元（Ad units）

打开 **Ad units**，顶部下拉选应用。表里通常可见：状态、名称、**Ad unit ID**、格式、已配网络数、参与的 mediation group 数。

点广告单元名称可改该格式设置，例如：

- **Rewarded**：奖励名称、数量、capping / pacing  
- **Interstitial**：展示频次相关 capping / pacing  
- **Banner**：刷新间隔等  

新建：**Create ad unit** → 唯一名称 + 格式 → 全新配置或从同格式已有单元复制 → Save。

> SDK 按「指定广告单元」加载时，需要把 **Ad unit ID** 传给对应 API（官网注明常见要求 LevelPlay SDK **8.4.0+**）。个人起步若只用默认单元，先确认后台默认单元已 Active，再在客户端接对应格式。

## 4. 应用侧常见配置（控制台）

| 项 | 做什么 | 备注 |
|----|--------|------|
| SDK Networks | 激活各广告网络、填 App ID / Placement | 客户端还要装 Adapter，见 [mediation-networks](mediation-networks.md) |
| Instances | 为网络建瀑布实例 / Bidding 实例 | 调 eCPM 与填充 |
| Placements | 命名激励/插屏等展示点，可配奖励与频控 | Advanced：[placements](https://docs.unity.com/en-us/grow/levelplay/platform/settings/advanced) |
| Capping & pacing | 限制展示/点击频率，避免伤留存 | 与广告单元、Placement 联动 |
| Segments | 按规则分用户群，套不同广告策略 | 个人可后做 |
| Rewarded / S2S callback | 激励发奖走自家服务器时打开 | 防客户端篡改奖励 |

隐私相关（COPPA、CCPA、ATT/UMP 等）按地区与应用受众在应用设置与客户端一并处理，见 [ops/privacy](../../ops/privacy.md)。

## 5. 个人最小路径

1. New App → 拿 **App Key**  
2. 至少激活一种 Ad unit（建议先 **Rewarded** 或 **Interstitial**）  
3. 接好 SDK Init + 一种格式 → [testing](testing.md)  
4. 再加 Unity Ads 等网络与 Instances  

返回：[概览](index.md) · [平台地图](portal-map.md) · [报表](reporting.md)
