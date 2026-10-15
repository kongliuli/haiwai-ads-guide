# 结算与收款

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：AdMob [Payments](https://support.google.com/admob/answer/2772140) / [Payment thresholds](https://support.google.com/admob/answer/2772208) / [Select payment form](https://support.google.com/admob/answer/2772229) · 各平台控制台 Payments / Billing（MAX、Unity、Meta）· 本站 [平台总览](../platforms/overview.md)

**起付线、可用收款方式、税表与持有(hold)状态以各平台控制台当时显示为准。** 下表是个人开发者学习用的常见对照，不是官网承诺；政策会变，开户前请再点开 Payments 页核对。

## 各平台常见对照

| 平台 | 常见收款方式（视国家/地址而定） | 常见起付线（示意） | 周期速记 | 官方入口 |
|------|--------------------------------|-------------------|----------|----------|
| Google AdMob | 电汇(Wire)、EFT/SEPA、部分地区支票等；部分地址可经第三方账户收 USD | 报道货币为 USD 时，支付门槛常见 **$100**；选支付方式门槛常见更低（如 $10） | 按月；约每月 21 日前后发起（无 hold 且达门槛） | [Payments and transactions](https://support.google.com/admob/answer/2772140) · [Thresholds](https://support.google.com/admob/answer/2772208) |
| Google AdSense | 与 Google 收款体系同源（网站变现） | 同报告货币门槛逻辑，以 AdSense Payments 为准 | 同 Google 月结节奏 | [AdSense 付款帮助](https://support.google.com/adsense/topic/1319758) · 本站 [付款要点](../platforms/adsense/payments.md) |
| AppLovin MAX | PayPal、银行电汇等（以后台可选列表为准） | 常见随方式约 **$20–$150**（示意） | 以后台 Billing 为准 | [dash.applovin.com](https://dash.applovin.com/) → Account / Payments |
| Unity Ads / LevelPlay | 电汇、PayPal 等 | 常见满 **$100**（示意） | 以后台为准 | Unity Grow / LevelPlay 账户 Payments |
| Meta Audience Network | PayPal、银行电汇等 | 常见满 **$100**（示意） | 以后台为准 | Meta for Developers / Monetization 收款设置 |

说明：

- 「常见」≠「你账号一定有」：可选方式取决于**付款地址国家**、主体类型（个人/公司）、税务信息是否齐全。  
- 未达起付线通常**结转下月**，不是清零。  
- 有支付 hold（地址验证、税表、政策审查）时，即使余额够也不会打款。

## 国内个人开发者：常见收款路径提示

以下为实务中常被讨论的路径，**不是税务或外汇建议**；是否合规、费率、限额以银行/牌照机构与平台条款为准。

1. **Google（AdMob / AdSense）**  
   - 控制台可选方式以你的付款资料国家为准。  
   - 国内个人常见做法：用电汇到支持接收 Google 付款的账户，或通过平台允许的第三方收款账户（例如部分地区用 Payoneer 等接收 USD）——**以 AdMob「How you get paid」里实际可选选项为准**。  
   - 税表、PIN 地址验证未完成前，往往无法正常出款。

2. **AppLovin / Unity / Meta**  
   - 若后台提供 **PayPal**：许多个人会优先用 PayPal 收 USD，再按 PayPal 规则提现或消费。  
   - 若只有 **Wire**：准备好英文账户名、银行地址、SWIFT 等；中间行费用可能被扣，到账天数以银行为准。  

3. **多平台共用一张「收款身份」**  
   - 尽量让各平台付款主体姓名与收款账户一致，减少 hold。  
   - 公司主体与个人主体不要混用同一套说不清的账户。

4. **算清「到手」**  
   - 平台手续费、PayPal/电汇中间行、汇率、提现费都会吃掉一部分；对照表里的起付线是「平台起付」，不是「你银行卡净入账」。

## 个人开发者上线前检查

- [ ] 控制台 Payments 无红色 hold / 待验证  
- [ ] 税务信息（如 W-8BEN 等，若平台要求）已提交且状态正常  
- [ ] 收款方式已选，且试算/预览信息无误  
- [ ] 改付款信息避开平台「当月截止日」（AdMob 常见要求约 20 日前改完才进当月批次）  
- [ ] 保留账单与到账记录，便于对账与报税  

## 相关页

- [平台总览](../platforms/overview.md) · [AdSense 付款与税务要点](../platforms/adsense/payments.md)  
- [隐私合规](privacy.md) · [ads.txt](ads-txt.md)
