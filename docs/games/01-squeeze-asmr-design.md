# App #1 设计文档：Squeeze ASMR（挤牙膏解压）

> **Working Title**：`Squeeze ASMR` / `Toothpaste Relax`  
> **定位**：首款上线，验证 **MAX 变现 + 买量素材 CTR + 共享壳**  
> **平台**：iOS + Android，海外 Tier1/2 优先  
> **技术**：Unity + .NET 推荐；MAUI Blazor 可作 POC  
> **关联**：[技术选型](../tech-stack-unity-vs-maui.md) · [广告变现](../app-store-ad-monetization.md)

---

## 1. 产品概述

### 1.1 一句话

单指竖向滑动「挤」管状物，观看形变与挤出物，配合音效与震动，**无失败、无关卡压力** 的解压体验。

### 1.2 目标用户

- 18–35，TikTok/Shorts 刷解压视频人群  
- 通勤/睡前 **1–3 分钟** 碎片使用  

### 1.3 国内参考（学机制，不抄素材）

抖音「挤牙膏 / Antistress」类：300+ 子玩法中的 **单个子玩法独立出海**。

### 1.4 成功指标（Soft Launch 4 周）

| 指标 | 目标 |
|------|------|
| Store CVR | ≥ 35% |
| D1 | ≥ 28%（无失败设计，应偏高） |
| D7 | ≥ 10% |
| Sessions/DAU | ≥ 2.0 |
| ARPDAU | ≥ $0.04 |
| Imp/DAU | 6–10（Banner + 偶尔 Interstitial） |

---

## 2. 核心循环

```
启动 → 选「管子」皮肤（3 个免费）
     → 按住拖动挤压力度 → 形变 + 挤出 + 音效 + Haptic
     → 挤空 → 庆祝动画 → 「再挤一支」/ 换皮肤
     → 每 3 支 Interstitial；新皮肤 = Rewarded 或 IAP
```

**Session 设计**：无 Game Over；用户自停。通过 **新管子/新颜色** 驱动继续。

---

## 3. 玩法机制

### 3.1 输入

| 输入 | 行为 |
|------|------|
| 按住并上下拖 | `squeezeAmount = clamp(dragDelta · sensitivity)` |
| 快速滑动 | 挤出「多段」blob，额外 satisfying 音效 |
| 松开 | 压力缓慢回弹（spring） |

### 3.2 形变（Unity 实现）

| 方案 | 说明 |
|------|------|
| **Sprite 网格 deform（推荐）** | 管身用 **2D Sprite + 顶点偏移** 或 `UnityEngine.U2D` 简单 mesh |
| Spine / 序列帧 | 成本高；MVP 不用 |
| Shader | `squeezeAmount` 驱动 UV 压缩；适合光滑牙膏体 |

**挤出物**：ParticleSystem 或预制 `Blob` pooling；颜色 = 当前 toothpaste 色。

### 3.3 内容解锁

| 类型 | 数量 MVP | 解锁 |
|------|----------|------|
| 管子外形 | 6 | 3 免费 + 3 Rewarded |
| 牙膏颜色 | 8 | 进度挤空 N 次解锁 |
| 背景 | 4 | 默认 1 + Rewarded |

### 3.4 可选轻量 Meta（v1.1）

- **Daily Tube**：每日一种限定花纹  
- **Collection**：图鉴 %（挤过即点亮）  

---

## 4. UI / UX

### 4.1 屏幕结构

```
┌─────────────────────────────┐
│  [Settings]     [Gallery]   │
│                             │
│         ┌─────────┐         │
│         │  TUBE   │         │
│         │  BODY   │         │
│         └────┬────┘         │
│              ▼ blob         │
│                             │
│   ◀ Swipe tube type ▶       │
├─────────────────────────────┤
│  Banner Ad (MREC 可选)      │
└─────────────────────────────┘
```

### 4.2 文案（英文）

- 标题：**Squeeze ASMR - Relax & Chill**  
- 副标题：*No wifi needed. Pure satisfying squeeze.*  
- 权限：仅振动；**不声明 Offline** 若广告需网络  

### 4.3 无障碍

- 支持 **单手** 操作区在屏幕中下 60%  
- `Reduce Motion` 时减弱粒子  

---

## 5.  monetization

| 格式 |  placement | 频次 |
|------|------------|------|
| **Banner** | 底部常驻 | 始终（可 Remote Config 关） |
| **Interstitial** | 挤空第 3、6、9… 支 | 冷却 ≥90s |
| **Rewarded** | 解锁管子/背景 | 用户主动 |
| **IAP** | Remove Ads `$2.99` | 可选 v1.0 |

**D1 降频**：Remote Config `interstitial_every_n_tubes_d1 = 5`。

---

## 6. 技术设计

### 6.1 Unity（推荐）

```
Game.SqueezeAsmr/
├── Scenes/Main.unity
├── Scripts/
│   ├── SqueezeController.cs      # 输入 → squeezeAmount
│   ├── TubeDeformView.cs           # 形变表现
│   ├── BlobSpawner.cs
│   └── TubeCatalog.cs              # ScriptableObject 皮肤
├── Audio/                          # 挤压、弹出 WAV
└── Plugins/                        # 来自 Template：MAX, Firebase
```

**依赖 Template**：`MicroGame.Unity.Template`  
**引用 Core**：`AdPolicy`, `AnalyticsEvents`

**Package**：可选 `Nice Vibrations` 或 Android/iOS 原生 haptic

### 6.2 MAUI Blazor（POC 路径）

- **SkiaSharp** 绘制圆角矩形管身；`SKPath` 变形  
- `IDispatcher` 60fps 刷新  
- 广告：`CommunityToolkit.Maui` + 自绑 MAX（工期 +1–2 周）  
- **POC 成功标准**：手感和 Imp/DAU 接近 Unity 版的 80%  

### 6.3 存档

```json
{
  "tubesUnlocked": ["classic", "striped"],
  "totalSqueezes": 42,
  "lastTubeId": "classic"
}
```

`PlayerPrefs` / MAUI `Preferences`

### 6.4 Analytics 事件

| 事件 | 参数 |
|------|------|
| `session_start` | `app_version` |
| `squeeze_complete` | `tube_id`, `duration_sec` |
| `unlock_tube` | `tube_id`, `via=rewarded\|progress` |
| `ad_impression` | `format`, `placement` |

---

## 7. MVP 范围

### 7.1 In Scope（v1.0，约 2–3 周 Unity）

- [ ] 1 种管形 + 形变 + 3 色牙膏  
- [ ] 6 皮肤（3 Rewarded）  
- [ ] Banner + Interstitial + Rewarded  
- [ ] MAX + Firebase + UMP/ATT  
- [ ] Settings + Rate Us + Remove Ads IAP（可选）  
- [ ] Cross-Promo 占位 UI（第二款上线前 hidden）  

### 7.2 Out of Scope

- 300 合一子玩法  
- 账号登录、云存档  
- 社交分享（v1.1 加「录屏分享」引导）  

---

## 8. ASO / 买量

| 项 | 内容 |
|----|------|
| 关键词 | `asmr`, `squeeze`, `relax`, `fidget`, ` satisfying`, `stress relief` |
| 图标 | 截面牙膏 + 挤出物，高饱和 |
| 视频素材 | 3s 挤压特写 + 音效；竖屏 9:16 |

---

## 9. 风险

| 风险 | 缓解 |
|------|------|
| 竞品 `Antistress 3D` 众多 | 单玩法极致 + 素材差异化 |
| 会话过短 ARPDAU 低 | 皮肤收集 + Interstitial 自然断点 |
| MAUI 广告集成延期 | 默认 Unity 路径 |

---

## 10. 里程碑

| 周 | 交付 |
|----|------|
| W1 | 形变 playable + 音效 |
| W2 | 皮肤 + MAX 广告 |
| W3 | Template 整合 + Soft Launch（PH/CL） |
| W4 | 调 Remote Config + 素材测试 |
