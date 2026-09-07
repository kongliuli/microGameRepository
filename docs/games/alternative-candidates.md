# 其他候选游戏（Brief Spec）

> 除首发三款外的 **备选 / 第四款起** 方向；每项含 Unity/MAUI 适配与优先级  
> **关联**：[国内选题总表](../china-viral-games-localization-picks.md)

---

## 1. 优先级矩阵

| 游戏 | 魔性 | 海外竞争 | 开发量 | Unity | MAUI | 建议顺位 |
|------|------|----------|--------|-------|------|----------|
| **Daily Tile Match**（Wordle 式槽位三消） | ⭐⭐⭐ | 高 | 中 | ✅ | ⚠️ | #4 |
| **Spot the Difference**（怀旧找茬） | ⭐⭐ | 高 | 中 | ✅ | ✅ | #5 |
| **Draw Line Rescue**（画线物理） | ⭐⭐⭐ | 高 | 中 | ✅ | ❌ | #6 |
| **Impossible Quiz Rush**（脑腐问答） | ⭐⭐⭐ | 中 | 低 | ✅ | ✅ | #4–5 |
| **Bubble Pop Zen**（纯点击消除） | ⭐⭐ | 极高 | 低 | ✅ | ✅ |  filler |
| **Water Sort**（试管倒水） | ⭐⭐ | 极高 | 中 | ✅ | ⚠️ | ❌ 红海 |
| **Pin Pull / 拉针** | ⭐⭐ | 高 | 中 | ✅ | ❌ | #6 |
| **Merge Chain**（链式合成） | ⭐⭐ | 高 | 中 | ✅ | ⚠️ | #7 |

---

## 2. #4 推荐：Daily Tile Match

**Working Title**：`Match Daily` / `Tile Quest`

**机制**（学羊了个羊，不抄 IP）：
- 每日 **1 局** 固定种子关卡（全球同题）  
- 7 槽位 + 多层 tile；失败 1 次/天 或 Rewarded 重试  
- **无** 地狱第二关；难度曲线服务 D7 而非话题  

**差异化**：咖啡/太空主题；分享 `"Daily #128 cleared in 42s"`  

**Unity**：2D UI + Tile stack 数据结构  
**MAUI**：Blazor 网格可行  

**广告**：Daily 完成 → Interstitial；Hint → Rewarded  

**MVP**：2 周（若复用 #3 的 Grid 代码部分）

---

## 3. #5：Spot the Difference — Cozy Edition

**机制**：两图找 N 处不同；120s；错误点击扣时  

**素材**：自产 **欧美 retro** 插画（ diner, garage, campus）  

**Unity/MAUI**：均适合；MAUI 双图 overlay 点击  

**广告**：每 2 关 Interstitial  

**风险**：关卡美术产能 → 先做 **20 关 + procedural 微差**（色调 shift）

---

## 4. #5 备选：Impossible Quiz Rush

**机制**：10 道「反直觉」选择题/点击题；全对才过关；极难  

**参考**：国内《难度飙升》；海外 TikTok brainrot  

**Unity/MAUI**：纯 UI，**MAUI 最快**  

**广告**：失败 Interstitial；Skip → Rewarded  

**风险**：差评「impossible」→ 必须 **80% 可过 + 20% 真难**

---

## 5. Draw Line Rescue（画线存小人）

**机制**：画线挡障碍/引水流；物理模拟  

**Unity**：Physics2D + LineRenderer  
**MAUI**：❌  

**竞争**：`Love Balls`, `Happy Glass` 类多 — 需 **新梗皮肤**（救猫而非球）

---

## 6. 不建议近期做

| 游戏 | 原因 |
|------|------|
| Water Sort | 全球竞品饱和 |
| Screw Puzzle | Screwdom 等头部 |
| Suika / Merge Watermelon | 品类天花板 |
| 文字梗解谜 | 翻译成本 + 文化隔阂 |

---

## 7. 与首发三款的组合策略

```
Phase 1（0–3 月）  #1 Squeeze → #2 Catch → #3 Pantry
Phase 2（3–6 月）  #4 Daily Tile 或 Impossible Quiz（开发最快）
Phase 3            Spot Diff 或 Draw Line（需内容管线）
```

**Cross-Promo 顺序**：  
Squeeze（低门槛）→ Catch（趣味）→ Pantry（长 Session）→ Daily Tile（留存锚点）

---

## 8. 选型决策树

```
上一款 D1 已 ≥30%？
├─ 否 → 同品类微调，不急着开新品类
└─ 是 → 下一款选 Session 更长 or 留存更强
         ├─ 缺 D7 → Daily Tile / Pantry 类
         ├─ 缺买量素材 → Catch / Draw Line
         └─ 缺产能 → Impossible Quiz（UI only）
```

---

## 9. 文档索引

| App | 设计文档 |
|-----|----------|
| #1 Squeeze ASMR | [01-squeeze-asmr-design.md](./01-squeeze-asmr-design.md) |
| #2 Catch Rush | [02-catch-physics-design.md](./02-catch-physics-design.md) |
| #3 Pantry Sort | [03-pantry-sort-design.md](./03-pantry-sort-design.md) |
| 技术栈 | [tech-stack-unity-vs-maui.md](../tech-stack-unity-vs-maui.md) |
