# AppLovin MAX · Preparing mediated networks（准备网络）

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Android Preparing](https://support.applovin.com/en/max/android/preparing-mediated-networks) · [iOS Preparing](https://support.applovin.com/en/max/ios/preparing-mediated-networks) · [Unity Preparing](https://support.applovin.com/en/max/unity/preparing-mediated-networks)

核心 SDK 跑通后，收益靠 **mediation adapter + 网络自家 SDK**。官方 **Preparing mediated networks** 页可勾选网络并**生成** Gradle / Pod / Integration Manager 步骤——版本与仓库 URL 以该页当前输出为准；本页只抓个人开发者必知要点，并链回原文。

后台 Connect、Ad Unit Placement、各家 Bidding 字段见 [networks-bidding.md](networks-bidding.md)。

## 合规提醒（官网 Caution）

接入第三方 SDK 时，你与该网络共同负责合规处理用户/设备隐私选择与 flag。勿假设「挂上 adapter = 隐私已搞定」——见 [ops/privacy.md](../../ops/privacy.md)。

## 两种集成方式

| 方式 | 适用 | 注意 |
|------|------|------|
| **推荐：官方 adapter 包** | Android Gradle POM / iOS CocoaPods / Unity Integration Manager | POM/Pod 常**自动**拉上网络 SDK 与依赖 |
| **开源 adapter** | 要自管网络 SDK 版本时 | Android：[AppLovin-MAX-SDK-Android](https://github.com/AppLovin/AppLovin-MAX-SDK-Android)；须自己集成网络 SDK |

**禁止**改 adapter 的包名 / 名称——MAX 将无法识别，广告加载失败。

## 按平台怎么准备

### Android

1. 打开 [Preparing · Android](https://support.applovin.com/en/max/android/preparing-mediated-networks)  
2. 勾选要接的网络（Meta、Unity Ads、Pangle、Mintegral、Google Bidding…）  
3. 把页面生成的 `repositories { … }` 与 `dependencies { … }` 拷进 app 模块 `build.gradle`  
4. Sync；用 [Mediation Debugger](testing.md) 看 Completed / Incomplete  

个人起步常见片段形态（**勿盲抄版本**，以官网勾选结果为准）：

```groovy
repositories {
  google()
  mavenCentral()
  // 部分网络额外仓，例如：
  // maven { url "https://dl-maven-android.mintegral.com/repository/mbridge_android_sdk_oversea" }
  // maven { url "https://artifact.bytedance.com/repository/pangle" }
}

dependencies {
  implementation("com.applovin:applovin-sdk:+")
  implementation("com.applovin.mediation:facebook-adapter:+")
  implementation("com.applovin.mediation:unityads-adapter:+")
  // …
}
```

推荐用 adapter 的 `+` 或文档钉死版本，让 POM 带网络 SDK。

### iOS

1. 打开 [Preparing · iOS](https://support.applovin.com/en/max/ios/preparing-mediated-networks)  
2. 勾选网络 → 按生成的 `pod 'AppLovinMediation…Adapter'` 行写入 Podfile  
3. `pod install --repo-update`  
4. 补 SKAdNetwork / ATT（加网络后 ID 列表会变长）  

SPM / 手动路径见该页；个人项目优先 CocoaPods 生成片段。

### Unity

1. 菜单 **AppLovin → Integration Manager**  
2. Mediated Networks 区对目标网络点 Install / Upgrade，按提示 Import  
3. 部分网络（如 Google）会多出 App ID 等字段，填控制台值  
4. 细节与迁移说明：[Preparing · Unity](https://support.applovin.com/en/max/unity/preparing-mediated-networks)

未用 Integration Manager 时，仍须对照 Preparing + Debugger（见 Getting started checklist）。

## 与控制台的分工

Preparing **只解决工程依赖**。还要：

1. 各网络后台建 App / Placement（尽量为 MAX 单独一套 ID）  
2. MAX：**Manage → Networks** Connect  
3. **Ad Unit → Default Waterfall** 打开 Bidder Status 并填 Placement  

缺任一步 → Debugger 可能绿，但线上无竞价。流程与常踩坑：[networks-bidding.md](networks-bidding.md)。

## 起步选哪些网络

官网 Getting started：除 AppLovin 外先接约 **6 家**全球需求源（如 Google、Meta）。个人量小可先：

- Meta Audience Network  
- Unity Ads  
- Google Bidding / AdMob（若已有 Google 账号）  
- Pangle / Mintegral（按地区）  

包体与冷启动随 adapter 增加：用 Advanced Reporting 的 win rate / 收入再扩或砍。

## 版本怎么盯

1. **Mediation Debugger** 标红的「网络 SDK ↔ adapter」优先修  
2. 升 MAX 核心 SDK 时，常需**整组**升 adapter（回 Preparing 页或 Integration Manager）  
3. 个别 Bidding（如 Unity Ads Banner/激励）写死了最低 adapter——低于下限等于白接，见 [networks-bidding.md](networks-bidding.md)

## 官方入口（收藏）

| 平台 | Preparing 原文 |
|------|----------------|
| Android | https://support.applovin.com/en/max/android/preparing-mediated-networks |
| iOS | https://support.applovin.com/en/max/ios/preparing-mediated-networks |
| Unity | https://support.applovin.com/en/max/unity/preparing-mediated-networks |
| 各网络逐步指南 | https://support.applovin.com/en/max/mediated-network-guides/sdk-bidder-network-guides |

下一篇：[networks-bidding.md](networks-bidding.md) · [testing.md](testing.md)。返回：[getting-started.md](getting-started.md) · [portal-map.md](portal-map.md)
