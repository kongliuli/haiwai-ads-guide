# 善用聚合（Mediation）打破单一平台瓶颈

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：各平台 Mediation / Bidding 文档综合（见 [选题对照](../catalog.md)）

## 何时上聚合

海外 **DAU 大致 > 1000** 之后，不要只接一家广告 SDK。

单网络的填充与出价会随地区、时段、广告位波动。用聚合让多家源对同一次展示机会竞价，通常能抬高有效 eCPM。

## 主聚合层（三选一）

不要两套主聚合并存（双初始化、包体、竞态）。

| 主聚合 | 适合 | 备注 |
|--------|------|------|
| AdMob Mediation | 已用 AdMob 的工具/内容 App | 与 Google 账号一体 |
| AppLovin MAX | 游戏、激励/插屏向 | Bidding 与 eCPM 表现强 |
| Unity LevelPlay | Unity / 游戏向 | 与引擎集成顺 |

## 常见 Bidding 广告源

在主聚合后台配置（以各平台 Mediated networks 列表为准）：

- Meta Audience Network  
- Unity Ads  
- Pangle（穿山甲海外）  
- Mintegral  
- 以及主聚合自有网络  

配置合理时，相对单网络常见能把整体 **eCPM / 收益抬约 20%–50%**（视地区、广告位、是否真 Bidding 而定）。

## 实施注意

1. 先稳定单网络，再开 Mediation。  
2. Meta AN 现多要求经 Bidding 聚合接入。  
3. 维护 **app-ads.txt**（应用）或 **ads.txt**（网站）（见 [ads.txt](../ops/ads-txt.md)）。  
4. 同步做 ATT / UMP 等隐私合规（见 [隐私合规](../ops/privacy.md)）。  
5. Adapter 越多包体与初始化越重，按收益贡献裁剪。  
6. Meta AN 经聚合步骤见 [via-mediation](../platforms/meta-an/via-mediation.md)。

返回：[平台总览](../platforms/overview.md)
