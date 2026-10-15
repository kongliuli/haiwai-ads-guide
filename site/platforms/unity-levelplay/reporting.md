# LevelPlay · 报表要点

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Measurement and reports](https://docs.unity.com/en-us/grow/levelplay/platform/measurement) · [Performance reports](https://docs.unity.com/en-us/grow/levelplay/platform/measurement/performance-reports) · [Schedule custom reports](https://docs.unity.com/en-us/grow/levelplay/platform/measurement/schedule) · [Reporting 总览](https://docs.unity.com/en-us/grow/levelplay/platform/measurement/reporting)

上线后用控制台看钱与填充是否正常。个人开发者优先 **Performance reports**；深度透视与定时邮件按需再开。

## 报表入口（对照官网）

| 工具 | 用途 | 个人优先度 |
|------|------|------------|
| **Home** | 变现/获客概览（可关联 Unity Ads 账户看整体） | 高（扫一眼） |
| **Performance reports** | 收入、eCPM、展示、填充相关指标，可筛应用/国家/网络/格式 | **最高** |
| **Real-time pivot** | 近实时切片（mediation / exchange / direct 等） | 中 |
| **Cohorts** | 按用户群看留存与变现趋势 | 低（有量再看） |
| **Report Generator / 定时报表** | 自定义指标与维度，邮件日/周/月送达 | 中（省得每天登录） |
| **Activity logs** | 约 90 天内谁改了瀑布、广告单元、A/B、网络等 | 排查配置时用 |

路径示意（菜单名以后台为准）：**Mediation → Reports → Performance**；定时报表常见在 **Monetize → Report Generator**。

## Performance reports 怎么用

1. 打开 Performance，切 **Graph** 或 **Table**  
2. 用筛选：日期、平台、广告格式、网络、应用、国家等  
3. **Metrics** 一次最多约 **8** 个（如 revenue、eCPM、impressions、sessions 等）  
4. 需要存档：**Export**；常用筛选点 **Save**，之后从 Saved reports 调出  

Table 视图里的数字一般是当前筛选下的合计（例如某广告源总收入），与 Graph 共用同一套 breakdown / filter。

## 定时自定义报表（摘要）

1. Report Generator → **New Report** → 配好维度、指标、筛选、日期范围 → **Save**  
2. 打开 **Scheduled On**，选 Daily / Weekly / Monthly（常见投递约 **10:00 UTC**）  
3. **Recipients** 可填账号内用户或任意邮箱；报表名会进邮件，起名写清楚  

日期预设常见：Yesterday、Last 7/14/30 days、This/Last Month、自定义（文档常见最长约一年）。

## 个人怎么读数

| 看什么 | 粗判 |
|--------|------|
| Revenue + eCPM | 是否在涨；某网络是否拖后腿 |
| Impressions / Fill 相关 | 是否「有请求无填充」或某市场挂了 |
| 按 Network breakdown | 新接的 adapter 是否真的在贡献 |
| 按 Country | 是否某国填充/eCPM 异常（合规或商店问题） |

改完瀑布或 Instances 后，用报表对比前后几天，并对照 [Activity logs](https://docs.unity.com/en-us/grow/levelplay/platform/measurement) 确认改动生效日期。

## 与 API

需要拉进自家 BI 时，用官网 [Reporting API](https://docs.unity.com/en-us/grow/levelplay/platform/api)（先鉴权再拉数）。个人站内不展开实现。

返回：[platform-basics](platform-basics.md) · [概览](index.md) · [平台地图](portal-map.md)
