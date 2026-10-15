# ads.txt 与 app-ads.txt

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：IAB [ads.txt / app-ads.txt](https://iabtechlab.com/ads-txt/) · [app-ads.txt 规范](https://github.com/InteractiveAdvertisingBureau/Supply-Chain-Validation/blob/main/app-ads.txt.md) · AdMob [Help：Set up app-ads.txt](https://support.google.com/admob/answer/9363762) · [Android](https://developers.google.com/admob/android/app-ads) / [iOS](https://developers.google.com/admob/ios/app-ads)

个人开发者常把「SDK 接好了却填充差」怪到代码上，其实很多是 **授权卖方文件缺失或域名对不上**。本页说明是什么、怎么放、为何影响填充。

## 是什么

| 文件 | 场景 | 作用 |
|------|------|------|
| **ads.txt** | 网站 / 移动 Web | 在站点根域声明「谁有权出售我的广告库存」 |
| **app-ads.txt** | 商店分发的 App | 同一套「授权卖方」思路，文件挂在**开发者网站**根路径，供爬虫按商店里的开发者网址去抓 |

二者都是 IAB Tech Lab 的 **Authorized Digital Sellers** 体系，用来降低假冒库存（spoofing）：买家/平台只信任你公开列出的卖方。

一行的典型形态（示意）：

```text
google.com, pub-xxxxxxxxxxxxxxxx, DIRECT, f08c47fec0942fa0
```

字段大致是：广告系统域名、你的发布商 ID、关系（DIRECT / RESELLER）、可选认证机构 ID。各网络在控制台会给出**应粘贴的片段**，不要手编造。

## 怎么放

### 网站：ads.txt

1. 用纯文本创建 `ads.txt`。  
2. 放到站点**根**：`https://你的域名/ads.txt`（须公网可直接打开，Content-Type 一般为 text/plain）。  
3. 把 AdSense / 各广告网络提供的授权行贴进去并保存。  
4. 等平台爬取（常见数小时到一天量级）。

### 应用：app-ads.txt

1. 准备一个**稳定的开发者网站**域名（个人站、GitHub Pages、Firebase Hosting 等均可，关键是能在根路径放文件）。  
2. 在商店详情填写的「开发者网站 / 营销网址」必须是该域名（路径可深，爬虫按规范取 hostname）。  
3. 发布：`https://你的开发者域名/app-ads.txt`。  
4. 从 AdMob 等控制台复制含 `pub-…` 的片段；接入 Meta / MAX / 其他源时，把各平台要求的行一并写入。  
5. 在 AdMob 等后台查看 app-ads.txt 状态；可请求重新爬取。验证常见需 **最多约 24 小时**。

注意：

- 文件名必须是 `app-ads.txt` / `ads.txt`，不要改成 `app-ads.txt.html`。  
- 商店里填的域名与文件所在域名要**一致**（含 www 与否，按你实际填写对齐）。  
- 一个开发者域名可服务多款 App；改文件会影响共用该域名的全部应用。

## 为何影响填充 / 收益

| 情况 | 可能后果 |
|------|----------|
| 没有 app-ads.txt，或爬不到 | 部分买家/平台降低出价或拒绝购买，表现为**填充变差、eCPM 下滑** |
| 缺了某网络的授权行 | 该网络（或经它转售的需求）可能不参与或受限 |
| 商店网址与文件域名不一致 | 平台显示未验证 / 错误，授权不生效 |
| 仅直连 SDK、从未配授权文件 | 短期偶有填充，中长期在程序化需求侧更吃亏 |

对个人开发者：接 **Meta Bidding、多源聚合** 时，把 app-ads.txt 当成与 adapter 同级的必做项，而不是「有空再写」。

## 个人检查清单

- [ ] `https://域名/app-ads.txt`（或网站的 `/ads.txt`）浏览器可打开且为纯文本  
- [ ] 含当前主变现平台（如 Google）的 DIRECT 行，ID 无抄错  
- [ ] 已启用的 Meta / AppLovin / 其他网络所需行已按控制台说明添加  
- [ ] Play / App Store 开发者网站字段已更新并与线上一致  
- [ ] AdMob（及 Meta 等）控制台授权状态为通过 / 无持续报错  

## 官方入口

| 主题 | 链接 |
|------|------|
| IAB ads.txt 总览 | https://iabtechlab.com/ads-txt/ |
| app-ads.txt 规范（GitHub） | https://github.com/InteractiveAdvertisingBureau/Supply-Chain-Validation/blob/main/app-ads.txt.md |
| AdMob 帮助：设置 app-ads.txt | https://support.google.com/admob/answer/9363762 |
| AdMob 开发者：Android | https://developers.google.com/admob/android/app-ads |
| AdMob 开发者：iOS | https://developers.google.com/admob/ios/app-ads |

## 相关页

- [聚合策略](../mediation/overview.md)  
- [Meta 经聚合接入](../platforms/meta-an/via-mediation.md)  
- [隐私](privacy.md) · [结算](payout.md)
