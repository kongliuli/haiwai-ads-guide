# Meta Audience Network · 本地材料

> 编写模型: Composer (Cursor Agent) · 2026-10-15

## 官网 / 文档

| 用途 | URL |
|------|-----|
| 产品介绍 | https://www.facebook.com/audiencenetwork |
| 开发者文档 | https://developers.facebook.com/docs/audience-network |
| Android 加 SDK | https://developers.facebook.com/docs/audience-network/setting-up/platform-setup/android/add-sdk |
| iOS GitHub（SPM） | https://github.com/facebook/FBAudienceNetwork |
| iOS Releases | https://github.com/facebook/FBAudienceNetwork/releases |

## 推荐坐标

- Android：`com.facebook.android:audience-network-sdk:6.22.0`
- iOS：SPM `https://github.com/facebook/FBAudienceNetwork`（自 6.22.0 起强化 SPM；CocoaPods 逐步弃用）
- **接入建议**：经 AdMob / MAX / LevelPlay Bidding，勿长期单独直连

## 本目录文件

| 文件 | 来源 | 说明 |
|------|------|------|
| `audience-network-sdk-6.22.0.aar` | Maven Central | Android SDK |
| `maven-metadata.xml` | Maven Central | 版本索引 |
| `release-6.22.0.json` | GitHub API | Release 元数据（该 tag **无** binary asset） |
| `FBAudienceNetwork-6.22.0-src.zip` | GitHub tag archive | 极小（SPM 二进制仓结构）；**完整 iOS framework 请用 Xcode SPM 拉取** |

归档日期：2026-10-15

## 缺口说明

GitHub Release `6.22.0` 未附带可直链的 `.xcframework.zip`。第二批预备材料中 iOS 侧以 SPM 仓库地址 + Android AAR 为准；若后续官方放出手动 ZIP，再补入本目录。
