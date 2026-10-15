# AdSense · 站点审核与连接

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Connect your site to AdSense](https://support.google.com/adsense/answer/7584263) · [Check the status of your AdSense sites](https://support.google.com/adsense/answer/12170222) · [Sign up for AdSense](https://support.google.com/adsense/answer/10162)

要通过审核并出广告，核心是两件事：**把站点连上 AdSense（验证）**，再 **Request review（申请审核）**。本页用中文说明流程、状态含义与连接失败时怎么查；审批评语与时限以账号通知为准。

## 总流程（个人站）

1. 在 AdSense 添加站点 URL（注册时已填可跳过）。  
2. 在首页「连接网站」类卡片中选择验证方式并完成验证。  
3. 勾选确认 → **Verify** → **Request review**。  
4. （可选）按提示选择同意管理平台（CMP）相关选项后提交。  
5. 等审核；通常数天，个别情况约 **2–4 周**。状态见首页 Sites 卡片或 **Sites** 列表。

未通过审核前，往往**无法正常展示广告**。别用狂刷自己广告的方式「催审」。

## 常见验证方式

控制台会列出可选方式（以当前 UI 为准），常见包括：

| 方式 | 你做什么 | 注意 |
|------|----------|------|
| **广告 / 站点代码** | 把给定 snippet 放进页面 HTML（多在 `<head>`），建议要出广告的页面都带上 | 域名须与添加的站点一致；内网、需登录才能看的壳站抓取会失败 |
| **ads.txt** | 把控制台给出的行写入站点根目录 `ads.txt` | 已有 ads.txt 则追加；须公网可访问 `https://你的域名/ads.txt`。横切说明见 [ads.txt](../../ops/ads-txt.md) |
| **其它（如 meta 标签等）** | 按控制台当时提供的步骤粘贴 | 以账号指引为准，本站不枚举所有变体 |

验证通过 ≠ 审核通过：前者只证明「这是你的站」，后者还要看整站是否符合计划政策。

## Sites 列表里常见状态

摘自官方[站点状态说明](https://support.google.com/adsense/answer/12170222)的学习向归纳（文案可能随语言略有差异）：

| 状态（示意） | 含义 | 你可以做什么 |
|--------------|------|----------------|
| **Requires review** | 尚未进入/完成审核请求 | 先做完账号要求的任务，再点 Request review；任务未完成时强行申请可能一直停在准备态 |
| **Getting ready** | 正在检查 / 排队审核 | **不要**删站再重提（易拖慢）；把付款资料等首页待办做完；等邮件/状态变更 |
| **Ready** | 可以展示广告 | 去设 Auto ads / 广告单元；持续遵守政策，问题看 Policy center |
| 连接失败 / 无法确认代码 | 抓取不到验证标记 | 见下一节排查 |
| 其它（如需再次审核、不活跃等） | 以控制台说明与帮助文为准 | 按「Request a review」类文章操作，勿反复删建站点 |

## 连接失败时先查

官方[连接网站](https://support.google.com/adsense/answer/7584263)强调的常见点：

- [ ] URL 是否写对（含 `www` / 根域是否与实际上线一致）  
- [ ] 验证代码 / ads.txt / meta **是否已部署到公网**，用无痕或手机网络打开确认  
- [ ] 整站是否被密码、防火墙、地区封锁挡在爬虫外（审核需要可抓取内容）  
- [ ] CDN / 缓存是否还在吐旧 HTML（改完强制刷新或清缓存）  
- [ ] 是否只把代码放在内页，而首页/主入口仍无标记（按控制台要求覆盖范围）  
- [ ] ads.txt 路径是否在**站点根**，而不是子目录误放

## 审核在看什么（学习向）

- **整站**是否符合 [AdSense 计划政策](https://support.google.com/adsense/answer/48182) 与发布商政策，而不是「某一页贴了代码」。  
- 内容是否足够、可导航、非空壳采集；个人站自查见[政策红线清单](policies-checklist.md)。  
- 账号侧付款等设置任务是否已推进——有时站点会停在 Getting ready，直到其它任务完成。

被拒或之后被停投：到 **Policy center** 看问题说明，改完再按指引申请复查。见[政策中心概览](https://support.google.com/adsense/answer/9485926)。

## 相关本站页面

- [AdSense 概览与网站接入](index.md)  
- [Auto ads 与广告单元](auto-ads.md) · [付款与税务要点](payments.md)  
- [帮助中心栏目对照](portal-map.md)

返回：[平台总览](../overview.md)
