# AppLovin MAX · Getting started（七步起步）

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Getting started](https://support.applovin.com/en/max/getting-started)

官方把「从零到能赚钱」收成 **七步**。本页中文重写步骤与个人开发者注意点；SDK 细节进 [android.md](android.md) / [ios.md](ios.md)，加网络进 [preparing-networks.md](preparing-networks.md) / [networks-bidding.md](networks-bidding.md)，联调进 [testing.md](testing.md)。

**重要（官网原意）**：先看账号最佳实践，避免违规导致停服。AppLovin **不在** Google Families Self-Certified Ads SDK 名单；面向儿童或含儿童内容的应用须遵守 Play Families 政策，且只能用名单内广告 SDK——详见各平台 Privacy 页与本站 [隐私](../../ops/privacy.md)。

## Step 1：账号

1. 注册 AppLovin 账号；完成认证后方可使用 MAX。部分账号需人工批准后才能走完设置。  
2. **付款**：Account → Payments → Info 填收款信息（AppLovin Exchange / Ads Manager 展示由 AppLovin 直接结算）。常见问题见官网 monetization payment FAQ；本站摘要：[结算](../../ops/payout.md)。  
3. **开发者域名**：Account → General → Basic Info → Domain 只填根域（如 `mywebsite.com`）。该域应与商店 listing 一致，并托管 `app-ads.txt`，方便广告主校验。见 [ads.txt / app-ads.txt](../../ops/ads-txt.md)。

## Step 2：建 Ad Unit

控制台路径：**MAX → Mediation → Manage → Ad Units**。

1. **加应用**：选 Android / Fire OS / iOS；已上架可搜店名选中，未上架可 **Manually Add Your Package Name**（大小写与工程一致）。  
2. **加广告位**：选格式、起名。官网强烈建议：**每个格式每个 App 只用一个 Ad Unit ID**，便于始终有缓存、少占带宽。  
3. 记下 **Ad Unit ID**（集成时要用）。首次建号可先跳过 Waterfall，后面 Step 6 再配。

## Step 3：集成 SDK 与网络

在接任何 mediated 网络前：先在该网络注册、建 App/广告位，并获准出广告。建号困难可查 [Mediated network guides](https://support.applovin.com/en/max/mediated-network-guides/sdk-bidder-network-guides)。

### 核心 SDK

按平台读 Integration（本站深页）：

| 平台 | 官方 | 本站 |
|------|------|------|
| Android | [Integration](https://support.applovin.com/en/max/android/overview/integration) | [android.md](android.md) |
| iOS | [Integration](https://support.applovin.com/en/max/ios/overview/integration) | [ios.md](ios.md) |
| Unity / Flutter / RN | Support Center → SDK integration guides | 见 [portal-map.md](portal-map.md) |

共性要求：

1. 用 Account → General → **Keys** 里的 SDK Key 初始化  
2. **启动时尽早** `initialize`，给各网络缓存时间  
3. （可选）开启 Ad Review，在控制台审创意  
4. Terms & Privacy Policy Flow；iOS 再配 ATT  

### 支持的网络

Adapter、兼容版本、Gradle/Pod 勾选生成：各平台 **Preparing mediated networks** → 本站 [preparing-networks.md](preparing-networks.md)。

### 不支持的（Custom）网络

走自定义 SDK 连接；官方不排障。见官网 Integrating custom SDK networks；Custom 一般**不能**进 in-app bidding / auto-CPM。

## Step 4：测集成

上架前用官方工具验通，见 [testing.md](testing.md)：

| 工具 | 用途 |
|------|------|
| **Demo app** | 官方示例工程当蓝图；可挂网络 SDK 看各格式回调 |
| **Mediation Debugger** | 看 adapter 是否装齐、版本是否匹配；可打测试广告 / 看 live waterfall |
| **Test mode** | 提高测试期填充概率；**不计**展示/点击/收入 |
| **Creative Debugger** | 抓创意问题并报给 MAX（本站暂未专篇） |

排障仍无解时：提工单并附 Demo 实现、verbose 日志、Debugger 截图。

**上线前 checklist（官网压缩）**：

1. 请求广告前设好隐私相关 flag  
2. 先挂初始化完成监听，再设 Key 并尽早 init  
3. Init 后立刻开始加载插屏 / 激励  
4. 加载或展示失败：指数退避重试（有上限）  
5. 用户关闭插屏/激励后：**立刻**预加载下一支  
6. Banner / MREC **尽量常驻屏上**，刷新率交给 MAX；藏在内容后会被 viewability 规则判无效  
7. 未用 Unity Integration Manager 时：对照 Preparing + Debugger 核对各网络配置；从 AdMob 等迁来时**勿复用**旧 mediator 的 App ID / Mediation Group，易崩溃与报表错乱  

## Step 5：Connect 网络

**MAX → Mediation → Manage → Networks** → Connect，填 API Key / 凭证 → Save。成功多为绿勾；红/黄表示还需操作。AppLovin 需求默认已开。

只 Connect **不够**：还必须在 Ad Unit 的 Waterfall 里打开 Status（下一步）。细节：[networks-bidding.md](networks-bidding.md)。

## Step 6：配 Waterfall

每个 Ad Unit 配一套。Bidding 与传统网络按最高 CPM 竞价出展示。

**Default Waterfall**：Ad Units → 选广告位 → Default Waterfall。仅对已集成且已 Connect 的网络展开、填 Placement / Game ID 等，Status **On** → Save。非 Bidding 需手填 CPM（或靠 Auto-CPM）；优先开 **Bidder**。

**Custom waterfall**：高级定向 / 分群（如 LAT、高 ARPU）；未命中流量仍走 Default。见官网 Waterfall management。

起步建议（官网）：除 AppLovin 外再接约 **6 家**有全球需求的源（如 Google、Meta）；个人量小可先 3–4 家 Bidding 再扩。改 Waterfall 前尽量 A/B。`app-ads.txt` 写上 AppLovin 条目以扩大 Exchange 竞价面。

## Step 7：看报表

控制台 **Analyze**：Performance / Advanced / User Activity；可存视图、定时邮件、Compare Mode。另有 revenue / user-level Reporting API，可接 MMP。

个人开发者常用：Advanced Reporting 看 **fill rate / win rate**，砍掉长期零贡献网络（包体与启动成本会随 adapter 涨）。

## 本站阅读顺序

1. 本页七步  
2. [android.md](android.md) 或 [ios.md](ios.md)  
3. [preparing-networks.md](preparing-networks.md) → [networks-bidding.md](networks-bidding.md)  
4. [testing.md](testing.md) 验绿再放量  

栏目全表：[portal-map.md](portal-map.md)。返回：[MAX 概览](index.md)
