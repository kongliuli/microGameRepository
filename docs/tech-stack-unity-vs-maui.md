# 技术选型：Unity + .NET vs .NET MAUI Blazor

> **团队栈**：Unity + .NET；备选 .NET MAUI Blazor Hybrid  
> **场景**：海外小游戏独立 App × IAA 变现 × 多 App 矩阵

---

## 1. 结论（TL;DR）

| 维度 | **Unity + .NET（推荐主栈）** | **.NET MAUI Blazor Hybrid** |
|------|------------------------------|-----------------------------|
| 三款首发游戏覆盖 | ✅ 全部适合 | ⚠️ 仅 #1 #3 勉强；**#2 物理抓物不推荐** |
| AppLovin MAX / 广告 SDK | ✅ 成熟官方 SDK | ⚠️ 需 Xamarin/MAUI 绑定或 Web 广告（受限） |
| 物理 / 粒子 / ASMR 手感 | ✅ 2D/3D 完整 | ❌ 需 SkiaSharp + 自研，无 Box2D 级生态 |
| 买量素材录制 | ✅ 60fps 稳定 | ⚠️ WebView 层可能掉帧 |
| 与现有 .NET 技能复用 | ✅ C# 脚本 + 共享 Class Library | ✅✅ UI/业务全 C#，Blazor 复用 Web 经验 |
| 多 App 共享代码 | `MicroGame.Core.dll` | 同一套 Core + MAUI 壳模板 |
| 首包体积 | 40–80MB 常见 | 15–35MB 可能更小 |
| 上架风险 | 行业默认 | 商店对 WebView 游戏审核经验少，需自证非壳 |

**推荐架构**：

```
┌─────────────────────────────────────────────────────────┐
│  MicroGame.Core (.NET Standard 2.1)                   │
│  Analytics · AdPolicy · RemoteConfig · CrossPromo DTO   │
└───────────────┬─────────────────────┬───────────────────┘
                │                     │
        ┌───────▼────────┐    ┌───────▼────────┐
        │ Unity 壳模板    │    │ MAUI 壳（可选） │
        │ MAX · Firebase  │    │ 仅 App #1 试验 │
        └────────────────┘    └────────────────┘
```

**ponytail 决策**：矩阵主力 **Unity**；若团队 Blazor 极强、想验证 **#1 挤牙膏** 用 MAUI 做 **一个** POC，成功再决定是否扩——**不要用 MAUI 做 #2**。

---

## 2. Unity + .NET 具体怎么拆

### 2.1 仓库结构（monorepo 建议）

```
microGameRepository/
├── src/
│   ├── MicroGame.Core/              # netstandard2.1，无 Unity 依赖
│   ├── MicroGame.Unity.Template/    # 共享 Unity 工程壳
│   ├── Game.SqueezeAsmr/            # App #1
│   ├── Game.CatchPhysics/           # App #2
│   └── Game.PantrySort/             # App #3
├── docs/
└── tools/                           # 关卡 JSON 校验、CI
```

### 2.2 MicroGame.Core 放什么

| 模块 | 内容 |
|------|------|
| `AdPolicy` | Interstitial 冷却、D1 降频规则（Remote Config 数值模型） |
| `AnalyticsEvents` | 统一事件名：`level_start`, `ad_impression` |
| `RemoteConfigKeys` | 常量 + DTO 反序列化 |
| `CrossPromoConfig` | 互推目标 App、deeplink schema |
| `SaveData` | 可选：JSON 存档模型（Unity 用 PlayerPrefs 存字符串） |

Unity 侧通过 **预编译 DLL 引用** 或 **源码链接** 引入；Gameplay 仍在 Unity `MonoBehaviour`。

### 2.3 Unity 壳模板（每个 App 复用）

- AppLovin MAX 初始化（`MaxSdk.Initialize`）  
- Firebase Analytics + Remote Config  
- GDPR UMP + iOS ATT 延迟弹窗  
- Pause 菜单 + Cross-Promo 入口  
- 统一 `GameBootstrap` 场景  

单款游戏只替换：`Gameplay` 场景 + `Addressables` 资源组。

### 2.4 .NET 后端（可选，MVP 不需要）

首发 **无需 ASP.NET 服务端**；Daily 关卡可用 **本地 seeded random** 或 Remote Config JSON。  
日活上来后再加：Daily 关卡 CDN、排行榜 API。

---

## 3. .NET MAUI Blazor Hybrid 可行性

### 3.1 架构

```
MAUI App
├── MainPage : BlazorWebView
├── wwwroot/          # Blazor 组件 + CSS
├── Platforms/        # Android/iOS 原生入口
└── Services/
    ├── AdService     # 绑定 MAX（CommunityToolkit 或自写 Binding）
    └── Haptics       # 原生震动
```

渲染选项：

| 方案 | 适用 | 问题 |
|------|------|------|
| **Blazor + CSS 动画** | #1 挤牙膏（2D 形变用 SVG/CSS） | 精细 ASMR 手感难 |
| **SkiaSharp.Views.Maui** | #1 #3 网格整理 | 需自写触摸逻辑 |
| **JS interop + Pixi/Phaser** | 理论上可行 | 两套栈，调试痛苦 |
| **物理引擎** | #2 | ❌  practically 不做 |

### 3.2 广告 SDK

- AppLovin 提供 Android/iOS **原生 SDK**；MAUI 需 **Android Binding Library / iOS Binding** 或社区包  
- 文档与 Unity 相比 **少一个数量级**；出问题要自己啃  
- **Google Mobile Ads** 在 MAUI 有较多社区示例，但游戏 eCPM 通常低于 MAX 聚合

### 3.3 何时值得用 MAUI 试 #1

- 团队 **几乎不会 Unity**，但 **熟 Blazor + SkiaSharp**  
- 目标 **极小 APK**、玩法 **纯 2D 无物理**  
- 接受 **广告集成多 1–2 周** 风险  

---

## 4. 三款游戏 × 技术匹配

| App | Unity | MAUI Blazor | 说明 |
|-----|-------|-------------|------|
| **#1 Squeeze ASMR** | ⭐⭐⭐ | ⭐⭐ | MAUI+Skia 可做 MVP；音效/haptic Unity 更顺 |
| **#2 Catch Physics** | ⭐⭐⭐ 必须 | ❌ | Rigidbody2D / 自定义物理 |
| **#3 Pantry Sort** | ⭐⭐⭐ | ⭐⭐⭐ | 网格 + 拖拽；MAUI 可用 Skia 或 Blazor 布局 |

---

## 5. 构建与 CI（Unity 矩阵）

| 项 | 建议 |
|----|------|
| Unity 版本 | **2022.3 LTS** 或 **6000 LTS**（团队统一） |
| .NET | Unity 内置；Core 库 **netstandard2.1** |
| 出包 | Unity Cloud Build 或 GitHub Actions + `unity-builder` |
| 版本号 | 每 App 独立 `bundleId`，共享 `MicroGame.Core` semver |

---

## 6. 决策树

```
是否需要 2D 物理 / 粒子 / 复杂动画？
├─ 是 → Unity
└─ 否 → 团队是否熟 Blazor 且不愿学 Unity？
         ├─ 是 → MAUI 仅做 #1 POC（4 周上限）
         └─ 否 → Unity

是否同一矩阵 ≥3 款 App？
└─ 是 → 统一 Unity 壳 + MicroGame.Core（降低 MAX 集成次数）
```

---

## 7. 相关文档

- [App #1 挤牙膏 ASMR](./games/01-squeeze-asmr-design.md)
- [App #2 物理抓物](./games/02-catch-physics-design.md)
- [App #3 收纳整理](./games/03-pantry-sort-design.md)
- [其他候选游戏](./games/alternative-candidates.md)
