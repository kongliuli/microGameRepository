# App #2 设计文档：Catch Rush（物理抓物）

> **Working Title**：`Catch Rush` / `Shake & Catch`（避免直译「抓大鹅」）  
> **定位**：第二款；验证 **核心循环 + D1 + TikTok 传播素材**  
> **平台**：iOS + Android  
> **技术**：**Unity 必须**（2D 物理）；MAUI 不推荐  
> **关联**：[技术选型](../tech-stack-unity-vs-maui.md) · [国内选题](../china-viral-games-localization-picks.md#21-抓大鹅-)

---

## 1. 产品概述

### 1.1 一句话

玩家 **摇晃/颠** 容器，让物品跳动，在限时内 **点选指定物品** 放入收集槽；槽满即过关，**物理 + 手速 + 眼速** 结合。

### 1.2 与国内「抓大鹅」差异（合规 + 海外）

| 国内常见 | 本设计 |
|----------|--------|
| 鹅 IP | **中性物品**：玩具、食物、太空杂物 |
| 地域榜 | **Weekly Global Challenge** |
| 三消槽位 7 格 | **收集槽 3–5 格** + 同类合并消除（可选 v1.1） |
| 微信分享复活 | **Rewarded 加时 / 提示** |

### 1.3 成功指标

| 指标 | 目标 |
|------|------|
| D1 | ≥ 30% |
| D7 | ≥ 8% |
| 平均 Session | ≥ 8 min |
| ARPDAU | ≥ $0.05 |
| Imp/DAU | 8–12 |

---

## 2. 核心循环

```
选关 → 容器内生成 N 个物品（含目标物）
     → 玩家 Shake（加速度计）或 拖动摇晃容器
     → 点击目标物 → 飞入收集槽
     → 槽满 / 时间到 → 胜利 or 失败
     → 失败 → Rewarded 复活 / Interstitial
     → 下一关
```

**单局时长**：60–90s（Hyper 偏长，利于广告）

---

## 3. 玩法机制

### 3.1 操作

| 操作 | 平台 | 效果 |
|------|------|------|
| **摇手机** | 加速度计 | 对容器 Rigidbody2D 施加 `AddForce` |
| **拖动摇杆** | 无陀螺仪 / 平板 | UI 虚拟摇杆倾斜容器 |
| **点击物品** | 全局 | Raycast 选中；仅 **目标类型** 可收集 |
| **双击容器** | 可选 | 「颠一下」大 force（学抓大鹅 meme） |

### 3.2 物理参数（Unity Physics2D）

```
Container: Static collider（U 形槽）
Items: Dynamic Rigidbody2D, circle/box collider, friction 0.3–0.6
Gravity: -9.81（可调关卡的「飘」感）
Max angular velocity: clamp 防止飞出屏幕
```

**防作弊飞出**：容器口 Collider 宽度略窄；物品 Y > 上限 → 弹回。

### 3.3 关卡目标类型

| 类型 | MVP | 说明 |
|------|-----|------|
| **Collect X of type A** | ✅ | 如收集 5 个红色玩具 |
| Collect multiple types | v1.1 | A×3 + B×2 |
| 限时 | ✅ | 60s，最后 10s 加速 BGM |
| 干扰物 | ✅ | 相似颜色增加难度 |

### 3.4 难度曲线

| 关卡段 | 物品数 | 干扰 | 时间 |
|--------|--------|------|------|
| 1–5 | 8–12 | 低 | 90s |
| 6–15 | 15–20 | 中 | 75s |
| 16+ | 20–28 | 高 | 60s |

### 3.5 Meta（v1.1 Hybrid）

- **房间主题**：厨房 / 太空仓 / 玩具箱（换 Skin）  
- **Star 评级**：时间剩余 → 解锁新容器外形  

---

## 4. UI / UX

```
┌─────────────────────────────┐
│  Lv.12    ⏱ 0:45    ⭐⭐⭐   │
│  Collect: 🧸×5              │
├─────────────────────────────┤
│ ╭─────────────────────╮     │
│ │  ·  · 🧸 ·  ·  ·    │     │
│ │    ·   ·   ·  🧸    │     │
│ ╰─────────────────────╯     │
│      [═══ Shake Hint ═══]   │
├─────────────────────────────┤
│ Slot: [🧸][🧸][  ][  ][  ]  │
└─────────────────────────────┘
```

- 首关：**强制 Shake 教程**（Detect shake once）  
- 失败屏：大按钮 **Watch to +30s** / **Retry**  

---

## 5. Monetization

| 格式 | 时机 |
|------|------|
| **Interstitial** | 每 **2 关** 胜利后；失败 ≥2 次后 |
| **Rewarded** | +30s / 高亮目标物 5s / 复活 |
| **Banner** | 关卡间隙大厅（Gameplay 中不开） |
| **IAP** | Remove Ads；**Level Skip Pack**（可选） |

**D1**：Interstitial 每 **3 关**。

---

## 6. 技术设计（Unity + .NET）

### 6.1 场景与脚本

```
Game.CatchPhysics/
├── Scenes/Gameplay.unity, Hub.unity
├── Scripts/
│   ├── ShakeDetector.cs           # Input.acceleration
│   ├── ContainerTilt.cs             # 响应 shake
│   ├── ItemSpawnDirector.cs       # 关卡 JSON → 生成
│   ├── CollectibleItem.cs         # 点击 → fly to slot
│   ├── CollectionSlotController.cs
│   └── LevelData.cs                 # 纯 C#，可放 Core
├── Prefabs/Item_*.prefab
└── Levels/levels.json
```

### 6.2 关卡数据（JSON，可用 .NET 工具离线校验）

```json
{
  "id": 12,
  "timeSec": 75,
  "targets": [{ "itemId": "teddy", "count": 5 }],
  "spawn": [
    { "itemId": "teddy", "count": 7 },
    { "itemId": "ball", "count": 10 }
  ]
}
```

`MicroGame.Core` 可含 `LevelValidator`（.NET 控制台工具）。

### 6.3 性能

- 同屏 Rigidbody2D ≤ **30**  
- 静止 sleep：`Rigidbody2D.Sleep()`  
- 对象池：物品回收复用  

### 6.4 为何不用 MAUI

- 需稳定 **60fps 多体碰撞** + 加速度计低延迟  
- Blazor WebView **不适合** 实时物理  
- SkiaSharp 自研物理 = 重写 Box2D，不 lazy  

---

## 7. MVP 范围

### In Scope（3–4 周）

- [ ] 30 关 + 无限随机关（种子 random）  
- [ ] Shake + 虚拟摇杆  
- [ ] 5 种物品 × 3 色  
- [ ] 收集槽 + 胜负判定  
- [ ] MAX 全套 + Analytics  
- [ ] Cross-Promo → App #1 / #3  

### Out of Scope

- 真多人、PvP  
- 3D 视角（保持 2D 降本）  

---

## 8. ASO / 买量

| 项 | 内容 |
|----|------|
| 关键词 | `shake game`, `catch`, `physics`, `arcade`, ` satisfying` |
| 素材 | 15s：疯狂 shake → 抓住物品 → 胜利；**真实手机摇晃拍摄** |

---

## 9. 风险

| 风险 | 缓解 |
|------|------|
| 国内玩法雷同 | 换主题 + 槽位规则差异 + 自研关卡 |
| 物理卡顿低端机 | 物品上限 + Quality 档位 |
| 摇晃晕 | 可选关闭 shake，仅虚拟摇杆 |

---

## 10. 里程碑

| 周 | 交付 |
|----|------|
| W1 | 物理容器 + 点击收集 |
| W2 | 关卡 JSON + 30 关 |
| W3 | Shake + 广告 + Hub |
| W4 | Soft Launch + 素材 |
