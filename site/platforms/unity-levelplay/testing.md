# LevelPlay · 集成验证与测试套件

> 编写模型: Composer (Cursor Agent) · 2026-10-15  
> 对照原文：[Integration testing（Platform）](https://docs.unity.com/en-us/grow/levelplay/platform/get-started/integration-testing) · Unity [Integration Helper](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/integration-helper) · Android [Integration Helper](https://docs.unity.com/en-us/grow/levelplay/sdk/android/integration-helper) · Unity [Package integration · Test Suite](https://docs.unity.com/en-us/grow/levelplay/sdk/unity/package-integration)

上线前确认三件事：SDK/Adapter 装对、控制台网络配通、测试机能拉到广告。不要用正式流量在未上架包上狂刷。

## 三条验证路径

| 路径 | 在哪做 | 验证什么 |
|------|--------|----------|
| **Integration Helper** | 客户端代码 | 依赖、权限、SDK 与 Adapter 版本是否 VERIFIED |
| **LevelPlay Test Suite** | 客户端（Init 后弹出） | 已配广告源能否加载/展示，并看测试机信息 |
| **控制台 Test devices** | Dashboard | 指定 GAID/IDFA 只吃某网络测试广告 |

---

## 1. Integration Helper（依赖核对）

集成完成后调用一次，看日志里各网络是否为 **VERIFIED**。未打算接入的网络显示 **MISSING** 可忽略；意图接入却显示 **NOT VERIFIED** 再查依赖与配置。

**Unity：**

```csharp
LevelPlay.ValidateIntegration();
```

**Android：**

```java
LevelPlay.validateIntegration(context);
```

（旧版 SDK 低于 7.3.0 时可能要求传 Activity，以当前官网为准。）

日志底部常会打印本机 **GAID / Advertising ID**，可复制到控制台「测试设备」。

验证通过后**删掉** Helper 调用，勿留在正式包。

---

## 2. LevelPlay 集成测试套件（Test Suite）

在 **Init 之前** 打开开关，**OnInitSuccess 之后** 再启动套件。

**Unity：**

```csharp
LevelPlay.SetMetaData("is_test_suite", "enable");
// … 注册回调后 Init …
// OnInitSuccess 内：
LevelPlay.LaunchTestSuite();
```

**Android：**

```java
LevelPlay.setMetaData("is_test_suite", "enable");
// … Init 成功后：
LevelPlay.launchTestSuite(context);
```

用来逐个确认已在控制台激活的广告源是否能加载与展示。细节以各引擎「Test your integration」页为准。

---

## 3. 控制台：测试设备与强制某网络

### LevelPlay mediation 测试

1. 左侧进入 LevelPlay → **Settings → Test devices**（名称以后台为准）  
2. 选中应用 → **Add test device**  
3. 填设备名 + **Advertising ID**（可用 Helper 日志）+ OS → Save  
4. 在列表里选广告源与广告单元 → **Test ads**  

该设备会暂时主要吃该网络广告，便于确认配置。文档说明默认约 **一小时内** 恢复常规配置。

### ironSource Ads 网络测试

路径在 **ironSource Ads → Setup → Testing**：加测试设备后，对该设备上相关广告单元自动走测试内容；可用开关随时停/开。

---

## 推荐顺序（个人）

1. 控制台应用 + Ad unit + 至少一个网络（常含默认 Unity Ads）  
2. 客户端 Init 成功  
3. `ValidateIntegration` → 修 NOT VERIFIED  
4. 开 Test Suite 拉广告  
5. 需要钉死某网络时，再加 Test device + Test ads  
6. 发版前去掉 Helper / Test Suite 元数据与调试入口  

## 常见坑

- 未 Resolve Android 依赖却以为 Adapter 已装好 → Helper 报 NOT VERIFIED  
- 只装了客户端、控制台网络未 Login / 未填 Placement → 套件里该源失败  
- 测试机 GAID 填错（模拟器 / 多用户 / 重置广告 ID）  
- 正式包仍开着 `is_test_suite`  

返回：[unity-package](unity-package.md) · [android-native](android-native.md) · [platform-basics](platform-basics.md) · [平台地图](portal-map.md)
