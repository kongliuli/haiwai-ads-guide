# Google AdSense · 概览与网站接入

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[AdSense 代码说明](https://support.google.com/adsense/answer/9274634) · [连接网站](https://support.google.com/adsense/answer/7584263) · 控制台 [adsense](https://www.google.com/adsense/)

## 这是什么

AdSense 面向**网站与网页内容**变现：在页面放入广告代码后，Google 按上下文匹配广告。个人站长常用；与 AdMob 可共用同一 Google 支付资料。

## 你需要准备

- 独立域名站点，内容原创且符合 AdSense 政策  
- 能改 HTML 或 CMS（如在 `<head>` 插入代码）  
- 站点可被公网访问，便于审核抓取

## 推荐路径

1. 注册 AdSense，添加网站并按提示完成验证（代码片段 / ads.txt / meta 等）— 详见[站点审核与连接](site-review.md)  
2. 审核通过前可能无法正常出广告；保持内容与流量合规  
3. 在需要展示的页面放入**广告代码**或使用 Auto ads  
4. 用官方文档核对放置位置（通常在 `<head>` 与广告位 `<ins>`）；付款关卡见[付款与税务要点](payments.md)

## 代码形态（示例）

将 `ca-pub-XXXXXXXX` 换成你的发布商 ID：

```html
<script async
  src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-XXXXXXXX"
  crossorigin="anonymous"></script>
```

广告单元示例见仓库 `materials/sdk/adsense/adsense-sample.html`。

## 本站续篇

- [帮助中心栏目对照](portal-map.md) — 官方分类 → 本站页地图  
- [站点审核与连接](site-review.md) — 验证、Request review、状态含义  
- [Auto ads 与广告单元怎么选](auto-ads.md) — 自动 vs 手动、放置与审核注意  
- [个人站政策红线清单](policies-checklist.md) — 内容 / 无效流量 / 放置自查  
- [付款与税务要点](payments.md) — 门槛、PIN、税表与出款节奏  

## 注意

- AdSense **没有**传统移动原生 SDK；WebView 套壳强行塞广告极易违规  
- 政策违规会导致限制广告或封号，优先读帮助中心「政策」类文章  

返回：[平台总览](../overview.md) · [官方文档平台对照](../../portals.md)
