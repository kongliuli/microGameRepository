# App #3 设计文档：Pantry Sort（收纳整理）

> **Working Title**：`Pantry Sort` / `Shelf Satisfying`  
> **定位**：第三款；拉高 **Session 长度 + 女性向 ASO + D7**  
> **平台**：iOS + Android  
> **技术**：Unity 推荐；**MAUI + SkiaSharp 可行** 作 UI 重度备选  
> **关联**：[技术选型](../tech-stack-unity-vs-maui.md)

---

## 1. 产品概述

### 1.1 一句话

把 **杂乱货架/冰箱** 上的物品拖放到 **正确格位**（同类相邻、分区规则），全部摆齐即过关。

### 1.2 与国内「货柜整理」差异

| 国内 | 本设计 |
|------|--------|
| 货柜三消式消除 | **纯摆放对齐**（无三消，降低与 Goods Sort 同质化） |
| 中文梗 | 英文 UI；**超市/ pantry** 主题 |
| 无限关卡刷 | **章节制** 50 关 MVP + Daily Sort |

### 1.3 成功指标

| 指标 | 目标 |
|------|------|
| D1 | ≥ 32% |
| D7 | ≥ 12% |
| 平均 Session | ≥ 12 min |
| ARPDAU | ≥ $0.06 |
| Imp/DAU | 10–14 |

---

## 2. 核心循环

```
选章节关卡 → 看到乱架 + 阴影槽位提示
          → 拖拽物品到槽位（snap）
          → 放错：抖动反馈，可拖回
          → 全部正确 → 星星 + Satisfying 动画 + 音效
          → Interstitial → 下一关
```

**单关**：45–120s

---

## 3. 玩法机制

### 3.1 规则（MVP 仅一种）

**Category Sort**：  
- 槽位带 **图标标签**（Drinks / Snacks / Dairy）  
- 物品仅一种正确区域  
- 同区域内 **任意顺序** 即可（降低难度）

### 3.2 进阶规则（v1.1）

| 规则 | 说明 |
|------|------|
| **Size fit** | 大格放大盘子 |
| **Color line** | 同色必须同一行 |
| **Frozen** | 先整理上层才能动下层 |

### 3.3 关卡结构

```
ShelfGrid: width x height 格子
Cells: { slotId, acceptedCategory, occupiedItemId? }
Items: spawn list with start positions (可叠放显示乱)
```

### 3.4 难度曲线

| 阶段 | 格子 | 物品种类 | 干扰 |
|------|------|----------|------|
| 1–10 | 3×3 | 3 | 无标签闪烁 |
| 11–30 | 4×4 | 4–5 | 1 个错误类别诱饵 |
| 31–50 | 4×5 | 5–6 | 限时 120s |

### 3.5 Meta

- **房间章节**：Pantry → Fridge → Closet  
- **Star**：时间 + 移动次数  
- **Daily Sort**：与 UTC 日期绑定的固定布局（Wordle 式回访）

---

## 4. UI / UX

```
┌─────────────────────────────┐
│  Fridge · Level 18    ⭐⭐☆ │
├─────────────────────────────┤
│ [Dairy][Dairy][Snack]       │
│ [Drink][ ??? ][Snack]       │
│ [Drink][Snack][ ??? ]       │
├─────────────────────────────┤
│ 待摆放: 🥛 🥤 🍪 🧀 🍫      │
└─────────────────────────────┘
```

- **Drag & Drop**：`IBeginDragHandler` / 触摸 follow  
- **Snap**：距离 < 阈值 → 吸附动画 `DOTween` 0.15s  
- **完成**：全屏 `confetti` 粒子 + ASMR 「咔哒」  

---

## 5. Monetization

| 格式 | 时机 |
|------|------|
| **Interstitial** | 每 **2 关** 完成 |
| **Rewarded** | 提示正确槽位 3s / 跳关 |
| **Banner** | 关卡选择页 |
| **IAP** | `$3.99` 去广告 + 解锁 Fridge 章节提前 |

关卡多 → **Imp/DAU 天然高**。

---

## 6. 技术设计

### 6.1 Unity（推荐）

```
Game.PantrySort/
├── Scripts/
│   ├── GridBoard.cs
│   ├── DraggableItem.cs
│   ├── SlotValidator.cs
│   ├── LevelLoader.cs
│   └── DailyLevelGenerator.cs    # seeded by date
├── ScriptableObjects/ItemDef.asset
└── Levels/*.json
```

**渲染**：2D UI（Canvas）或 Orthographic 2D sprite grid — **无需物理引擎**。

**可选 Package**：`DOTween`（免费版）

### 6.2 MAUI 路径（团队偏 Blazor 时）

- `SkiaSharp.Views.Maui` 画格子 + 位图图标  
- 拖拽：`SKCanvas` touch + 命中测试  
- 关卡 JSON 与 Unity **共用** `MicroGame.Core` 模型  
- 广告：同 #1 MAUI 绑定方案  

**工期对比 Unity**：相近或略长（拖拽 polish 自研）

### 6.3 Daily 关卡生成（.NET 纯逻辑，放 Core）

```csharp
public static LevelLayout GenerateDaily(DateOnly date, int seedSalt)
{
    var rng = new Random(HashCode.Combine(date, seedSalt));
    // 固定难度，全员同题 → 可分享 "Daily #452"
}
```

### 6.4 Analytics

| 事件 | 参数 |
|------|------|
| `level_complete` | `level_id`, `time_sec`, `moves` |
| `level_fail` | `reason=timeout` |
| `daily_play` | `date` |

---

## 7. MVP 范围

### In Scope（3 周）

- [ ] Pantry 章节 50 关  
- [ ] Category Sort 规则  
- [ ] 拖拽 + snap + 完成动画  
- [ ] Daily 1 关  
- [ ] 广告 + Cross-Promo  
- [ ] 章节地图 UI  

### Out of Scope

- 3D 冰箱旋转  
- 多人对战  

---

## 8. ASO / 买量

| 项 | 内容 |
|----|------|
| 关键词 | `organizing games`, `sort`, `satisfying`, `pantry`, `relax`, `ASMR` |
| 受众 | Meta/TikTok **女性 25–44** 定向可测 |
| 素材 | 前后对比：乱 → 整齐；**无文字** 也可跑量 |

---

## 9. 风险

| 风险 | 缓解 |
|------|------|
| Goods Sort / Sort Master 竞品 | **章节叙事 + Daily**；无三消 |
| 关卡生产慢 | JSON 编辑器 + 程序化填充干扰物 |
| 拖拽手感差 | snap 阈值 A/B |

---

## 10. 里程碑

| 周 | 交付 |
|----|------|
| W1 | Grid + 拖拽 + 校验 |
| W2 | 50 关 + 地图 |
| W3 | Daily + 广告 + Soft Launch |
