# AdMob · 测试广告与调试

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Android Test ads](https://developers.google.com/admob/android/test-ads) · [iOS Test ads](https://developers.google.com/admob/ios/test-ads) · Unity / Flutter 见各平台 `test-ads` 页

开发阶段的目标只有一件事：**稳定拉到测试创意、确认回调链路正确**，同时**绝不**用正式广告单元在未上架或调试机上狂刷。账号风险比「多测一次」贵得多。

相关：[广告格式](formats.md) · [Android 起步](android-getting-started.md) · [iOS 起步](ios-getting-started.md) · [栏目地图](portal-map.md)

---

## 1. 三条安全路径（任选，可组合）

| 方式 | 做法 | 适用 |
|------|------|------|
| **官方测试广告单元 ID** | 代码里写死 Google 公布的各格式测试 Unit ID | 日常开发、CI、模拟器 |
| **注册测试设备** | 用正式 Unit ID，但把设备标为 test device | 要验「真实单元配置」是否通 |
| **Demo App ID** | Manifest / Info.plist 暂用文档示例 App ID | 尚未建好自己的应用时 |

上架前检查：正式 App ID、正式 Unit ID、去掉调试用的测试设备注册与多余日志。

---

## 2. 测试广告单元（最常用）

Google 为 Banner / Interstitial / Rewarded / Native / App open 等维护一份**固定测试 Unit ID**。  
完整列表以官网为准（会随格式增减更新）：

- Android：[Test ads](https://developers.google.com/admob/android/test-ads)  
- iOS：[Test ads](https://developers.google.com/admob/ios/test-ads)  
- Unity / Flutter：同文档站平台切换下的 Test ads

要点：

- 测试单元返回的是**明确标为测试**的创意；填充通常比正式单元稳。  
- 不要把测试 Unit ID 打进生产包；用 Build Flavor / `#if DEBUG` / 远程配置切换。  
- 某格式「永远 no fill」时，先换回该格式的官方测试 ID，确认是单元配置问题还是代码问题。

---

## 3. 测试设备（Test devices）

当你必须用**自己的正式 Unit ID**联调（例如刚在控制台建好的单元、Mediation 组绑定）时：

1. 用带广告请求的 Debug 包跑一次，在 Logcat / Xcode 控制台找 SDK 打印的**测试设备哈希**提示（文案随 SDK 版本略有不同）。  
2. 按文档用代码注册（如 Android `RequestConfiguration.Builder.setTestDeviceIds`，iOS 等价 API），或在 AdMob 控制台把该设备标为测试设备。  
3. 成功后，正式单元也会下发测试创意，降低误点/无效流量风险。

注意：

- 同事每人一台设备要各自注册；模拟器与真机 ID 不同。  
- 发版流水线勿把「全家桶测试设备列表」留在 Release 配置里（至少拆到 debug-only）。

---

## 4. 调试时看什么

### Android（Logcat）

- 过滤 `Ads` / `GoogleMobileAds`（具体 tag 以当前 SDK 为准）。  
- 初始化完成日志：确认 App ID 已读到、Mediation adapter 状态。  
- `onAdLoaded` / `onAdFailedToLoad`：失败时记下 **error code / domain / message**，对照官方错误码表。  
- Mediation：看各 adapter 是否 init 成功、bidding 响应是否超时。

### iOS（Xcode / Console）

- 初始化与 load 回调同样以 error 对象为准。  
- Info.plist 缺 App ID 常在启动期直接暴露。  
- ATT / 同意未完成时，可能影响个性化，但测试单元仍应能填充——若测试单元也失败，优先查 Unit ID 与网络。

### 网络与环境

- 公司代理 / 抓包证书可能导致广告域名失败；先关代理复现。  
- 系统时间错误、极端省电杀后台，会导致加载超时或展示失败。  
- 模拟器可以测通路；**激励视频完播、部分 Mediation 源**仍建议真机。

---

## 5. 常见失败对照

| 现象 | 先查 |
|------|------|
| 崩溃提示 Missing application ID | Manifest / Info.plist 的 App ID meta |
| 一直 `no fill` / error code 3 | 是否正式单元+未上架；是否该换测试 Unit ID；地区与库存 |
| 仅正式单元失败、测试单元成功 | 控制台应用关联、商店链接、单元状态、Mediation 组绑定 |
| Mediation 源永不填充 | Adapter 依赖、对方后台凭证、测试设备是否被该源识别 |
| 展示后立即关闭 / 黑屏 | 生命周期：Activity/VC 是否在 show 时仍在前台；开屏是否与启动页抢焦点 |
| 「有广告但不计费」焦虑 | 测试创意本身不计生产收益，属预期 |

---

## 6. 与隐私 / 同意的顺序

EEA/UK 等地区：按官方建议在**请求广告前**完成 UMP 同意流程，并尊重 `canRequestAds` 一类门闸。  
测试期也建议把 UMP 跑通（可用调试地理等选项，见 [隐私与 UMP](privacy-ump.md)），避免「调试时能出广告、上架欧洲包却静默无 fill」。

---

## 7. 上架前测试清单（短）

- [ ] Release 使用正式 App ID + 正式 Unit ID  
- [ ] 已移除或门闸掉测试 Unit ID、调试用 test device 列表  
- [ ] 主路径：冷启动初始化 → 同意（若需要）→ load → 自然断点 show  
- [ ] 各已接格式至少真机走通一次成功回调  
- [ ] 若开了 Mediation：抽查 1～2 家源的 adapter 日志  

下一篇：[隐私与 UMP](privacy-ump.md) · 返回 [AdMob 概览](index.md)
