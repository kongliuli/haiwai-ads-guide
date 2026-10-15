# AdSense · 付款与税务要点

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Steps to getting paid](https://support.google.com/adsense/answer/1709858) · [付款主题](https://support.google.com/adsense/topic/1319758) · [美国税信息](https://support.google.com/adsense/answer/2490070) · [非美国税信息](https://support.google.com/adsense/answer/14131950) · [浏览账号 / Payments](https://support.google.com/adsense/answer/7107733)

本页用中文串起「怎么才能第一次收到 AdSense 款」——门槛、身份与地址验证、税表、出款窗口与常见 hold。**不是**税务或外汇建议；金额、扣缴率、可选收款方式以控制台 Payments 当前显示为准。

## 收款前要走完的台阶

官方把「第一次拿钱」拆成若干关卡（名称以控制台文案为准）。常见顺序：

| 台阶 | 大致在做什么 | 说明 |
|------|--------------|------|
| 1. 有可计费收益 | 站点通过审核并正常展示广告 | 见[站点审核](site-review.md) · [广告设置](auto-ads.md) |
| 2. 达到验证相关门槛 | 例如常见「收益到约 $10（或当地等值）」后确认付款姓名/地址 | 信息要真实，后面 PIN 寄往此地址 |
| 3. 身份验证（Identity） | 按要求在账号内上传证件类材料 | 官方常给约 **45 天**窗口；逾期可能影响出广告与付款 |
| 4. 地址 / PIN 验证 | Google 向付款地址邮寄 PIN，你在账号录入 | 邮寄可能需数周；自 PIN 生成起常有约 **4 个月**录入期限 |
| 5. 选择收款方式 | 余额达到「可选支付方式」门槛后，在 Payments 里选 EFT / 电汇等 | 可选列表取决于**付款地址国家** |
| 6. 达到支付门槛且无 hold | 月末余额 ≥ 支付门槛，且税表等 hold 已解除 | 常见支付门槛以报告货币计（USD 常见 **$100** 量级，以你账号为准） |

细节与当前门槛数字：打开[收款步骤](https://support.google.com/adsense/answer/1709858) 与账号 **Payments → Payments info**。

## 出款节奏（速记）

- AdSense 按**月**结算：若月末余额达支付门槛、且无付款 hold，通常在**次月约 21–26 日**之间发起付款。  
- 许多「当月能否进批次」相关的资料变更 / 税表提交，官方会强调尽量在**当月 20 日之前**完成；过了窗口往往滚到下一周期。  
- 未达门槛：余额**结转**，不是清零。

## 税务信息（要点）

- **不是人人都要交同一张表**；是否必须提交、交哪一国税信息，取决于你的付款资料所在地以及 Google 的扣缴/申报义务。见[美国税信息](https://support.google.com/adsense/answer/2490070) · [非美国税信息](https://support.google.com/adsense/answer/14131950)。  
- 入口通常在：**Payments → Payments info → Manage settings → Payments profile → 对应国家的 tax info**。  
- 提交后可在同一处查看可能适用的**预提税（withholding）**提示；具体税率与协定待遇以官方流程与税局规则为准，本站不解读个案。  
- 因缺税表导致的付款 hold：补齐过晚（例如晚于当月 20 日）可能错过当月批次。

## 常见 hold / 拿不到钱时先看

- [ ] 付款姓名、地址是否与证件 / 能收信地址一致  
- [ ] Identity、PIN 是否仍「待完成」  
- [ ] 税信息是否要求提交且已通过  
- [ ] 是否已选收款方式，且账户信息无红字错误  
- [ ] 政策或账号限制是否同时卡住广告与付款（见[政策清单](policies-checklist.md) · [政策中心](https://support.google.com/adsense/answer/9485926)）  
- [ ] 月末余额是否真的 ≥ 支付门槛

## 与 AdMob / 本站横切页的关系

Google 广告产品常共用或共用逻辑相近的**付款资料**；网站变现细节仍以 **AdSense Payments** 为准。多平台对照见 [结算与收款](../../ops/payout.md)。

## 相关本站页面

- [AdSense 概览](index.md) · [站点审核与连接](site-review.md)  
- [帮助中心栏目对照](portal-map.md)

返回：[平台总览](../overview.md)
