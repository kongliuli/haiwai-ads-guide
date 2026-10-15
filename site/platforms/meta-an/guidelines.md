# Meta AN · 政策与展示规范要点

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[AN Policy](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/an-policy) · [Dos and don’ts](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/an-policy/dos-and-donts) · [Best practices](https://developers.facebook.com/documentation/audience-network/optimization/best-practices) · [Layout](https://developers.facebook.com/documentation/audience-network/optimization/layout-best-practices) · [Audio](https://developers.facebook.com/documentation/audience-network/optimization/audio-best-practices) · [app-ads.txt](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/authorized-sellers-app-ads) · [COPPA](https://developers.facebook.com/documentation/audience-network/optimization/best-practices/coppa)

本文是**个人开发者红线摘要**，不是政策全文。上线、申诉、争议一律以官方政策页为准。

## 总原则

- 开发者须遵守适用法律、Audience Network 条款与开发者指南。  
- 使用 ads.txt / app-ads.txt 时，须**准确列入** Audience Network。见 [ops/ads-txt](../../ops/ads-txt.md)。  
- Meta 可拒绝、批准或移除发行商/应用；违规可暂停或终止服务。  
- 系统会分析点击、展示、安装等互动；高风险账户可能被限制或停用。

## 内容限制（节选）

应用/库存不得触及下列方向（细节与例外以原文为准）：

| 类别 | 含义（白话） |
|------|----------------|
| 社群守则 / 广告政策 / 内容变现政策 | 违规内容或屡次违规广告可导致移出 AN |
| 劣质或干扰性体验 | 半成品、误导体验、广告远多于内容等 |
| 违法商品服务 | 不得推广违法活动 |
| 暴力/骇人听闻、歧视 | 禁止 |
| 烟草、非法/处方药、不安全补剂、武器弹药爆炸物 | 禁止推广销售或使用 |
| 成人内容与服务 | 禁止 |
| 隐藏监控设备 | 禁止 |
| 一分钱/按次付费竞拍类模式 | 禁止 |
| 程序化投票信息、征集选民登记 | 禁止 |
| 真钱赌博/博彩 | 通常需书面许可 |
| 随机真钱抽奖免费体验 | 禁止 |
| 以 UGC 为主的应用 | 未获书面许可不得展示 AN 广告 |
| 买卖赞/粉/评论等社交互动 | 禁止 |
| 模仿 Meta 产品体验 | 禁止 |
| 误导性金融（如部分 ICO/二元期权等）、欺骗性就业 | 禁止 |
| 诈骗/骗取钱财或个人信息 | 禁止 |

## 实施限制（展示与交互）

个人开发者最易踩的坑：

1. **广告调用信息准确**：版位尺寸、应用标识等须对应已获批应用。  
2. **隐私政策**：应用须有能反映真实做法的隐私政策。见 [ops/privacy](../../ops/privacy.md)。  
3. **商店上架**：默认仅限已在 App Store / Google Play 上架的应用（除非书面批准）。Android **Early Access** 下不得走 AN 变现。  
4. **不得擅自改广告**：编辑、筛选、截断、最小化素材（含原生）均需事先书面许可；组件须完整可见。  
5. **不得抓取/缓存广告素材**做长期存储或索引。  
6. **防误点**：勿放在易误触位置；原生交互应落在标题、URL、CTA、图片等，而非空白背景。  
7. **区分广告与内容**：原生须可展开 AdChoices，并标明赞助/推广/广告。  
8. **勿挡重定向/弹层**；退出屏幕不能**唯一**依赖点广告。  
9. **禁止堆叠**：同一版位一次只填一条 AN 广告。  
10. **禁止诱导点击**、欺骗声明、强制/奖励「去点广告」。  
11. **禁止自动刷新** AN 广告；勿经带自动刷新的中介反复要同一素材。  
12. **禁止应用外/后台广告**；卸载后不得再投。  
13. **禁止间谍软件/恶意软件**相关宣传。  
14. **COPPA**：儿童相关须遵守 COPPA 与官方使用说明。

## 质量与真实性

- 勿滥发多版同质应用、勿缺截图/描述等基本商店信息。  
- 变现应用须归你所有/运营，或持有独家变现权，或有书面许可；需完成所有权验证。  
- **禁止无效流量**：爬虫、机器人、刷点击/展示、智能助手模拟真人等。  
- **禁止修改/逆向 SDK**。  
- 广告须基于真实设备、真实用户主动互动。  
- 勿伪造公司、财务、应用版本、商店信息等。  
- 异常行为可触发暂停或限制，供 Meta 核查。

## 激励视频 / 激励插屏附加政策（节选）

- **主动选择观看**：每条须让用户主动选看（如点播放、倒计时）；禁止「全场激励只给一次选择」；须说清奖励，且说明后可不退出应用即可关闭。  
- **禁止金钱/现金等价物奖励**（含可兑现金的礼品卡、加密货币、点数等）。  
- 投放须在体验断点后，或设频次上限并在商店说明使用激励广告。  
- 只能因**看完广告**发奖，不能因下载安装等下游转化发奖。  
- 奖励不可用户间转让；随机奖励须在选择观看**前**写明中奖概率（行动号召处，而非仅应用内总述）。  
- 看完须**立即**在本应用/网站内可兑奖。  
- 不得改关闭/跳过方式；用户拒绝激励后**不得**改弹普通插屏。  
- 未看完或通过举报/隐藏跳过 → **不得**发奖。

## 布局与音频

版位布局、音频自动播放等细项见官方：

- [Layout best practices](https://developers.facebook.com/documentation/audience-network/optimization/layout-best-practices)（[Android](https://developers.facebook.com/documentation/audience-network/optimization/layout-best-practices/android) · [iOS](https://developers.facebook.com/documentation/audience-network/optimization/layout-best-practices/ios)）  
- [Audio best practices](https://developers.facebook.com/documentation/audience-network/optimization/audio-best-practices)

格式级展示要求另见 [ad-formats.md](ad-formats.md)。

## 相关页

- [概览](index.md) · [经聚合 Bidding](via-mediation.md) · [报表](reporting.md) · [栏目地图](portal-map.md)  
- [隐私](../../ops/privacy.md) · [ads.txt](../../ops/ads-txt.md) · [结算](../../ops/payout.md)
