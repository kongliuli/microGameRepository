# 多 App 矩阵策略：每款小游戏独立上架

> **当前产品方向**：做一批有趣的小游戏，**每款单独形成一个 App** 上架商店，通过 IAA（+ 可选 IAP）变现  
> **面向市场**：海外用户  
> **关联文档**：[热度与粘性](./overseas-mini-games-heat-and-retention.md) · [广告聚合变现](./app-store-ad-monetization.md)

---

## 1. 结论摘要

| 维度 | 判断 |
|------|------|
| **模式** | 行业主流之一：Voodoo（60 亿+ 下载）、Rollic、SayGames、JindoBlu 均为 **多 App 矩阵**，而非单一聚合壳 |
| **与聚合 App 区别** | 每 App 一个核心玩法 + 独立 ASO 页；靠 **Portfolio LTV** 而非单 App 内换游戏 |
| **2025–2026 趋势** | 从「海量铺量」转向 **少而精 + Hybrid 化**；SayGames：更少项目、更深参与、更长生命周期 |
| **小团队关键** | **共享壳工程 / Mediation / 交叉推广 SDK**，把边际开发成本压到最低；失败作快速 Kill |
| **收入逻辑** | 单 App 多数会失败；靠 **1–2 款爆款** 养活矩阵；矩阵内 **Cross-Promo** 把流失用户导到下一款 |

---

## 2. 三种产品形态对比

| | **多 App 矩阵（当前方向）** | **单 App 聚合** | **Web 聚合（Poki）** |
|--|---------------------------|----------------|---------------------|
| 商店页 | 每款独立，关键词精准 | 一个「Mini Games」大页 | 无商店，靠 SEO |
| 用户预期 | 下载即玩某一类玩法 | 期待多款随便换 | 浏览器点开即玩 |
| 变现 | 每 App 独立 IAA | 换游戏 = 多插屏 | 页面广告 |
| ASO | 每 App 竞争细分词 | 抢大词 offline/mini games | N/A |
| 失败成本 | 单 App 可下架不影响其他 | 一个 App 失败 = 全灭 | 站点级风险 |
| 壁垒 | 选题 + 执行 + 发行节奏 | 内容数量 + 体验 | 品牌 + SEO |
| 典型代表 | Voodoo、Rollic、单款 Offline 衍生 | JindoBlu《Offline Games》合集 | Poki |

**何时选多 App 矩阵**

- 每款游戏有 **清晰单一卖点**，适合独立短视频买量素材  
- 团队能 **复用引擎/广告/Analytics 壳**，单款开发周期短（2–6 周）  
- 愿意接受 **80% 产品不赚钱**，用数据筛爆款  

**何时反而做聚合 App**

- 游戏偏短、偏同质，单款撑不起独立 Store 页  
- 想抢 `offline games` / `mini games` 等大词  
- 暂无买量能力，靠「游戏数量」做 ASO 长尾  

---

## 3. 行业怎么玩（海外发行商）

### 3.1 大厂 Pipeline

```
Ideation（大量点子）
    → Prototype / CPI Test（小预算验证）
    → Soft Launch（智利/菲律宾等测留存）
    → Global Launch + 买量放大
    → LiveOps / Hybrid 化（拉长 LTV）
    → Cross-Promo 导流到新 App
```

| 公司 | 策略要点 |
|------|----------|
| **Rollic** | 每月测试大量原型；从 Hyper 转 Hybrid；Color Block Jam 等靠 **IAP + 广告** 双轨 |
| **SayGames（2025）** | **减少项目数、加深合作**；ML 预测 + 更深 In-App Economy |
| **Voodoo** | 数百款 App；Cross-Promo 是核心——「让用户留在自家生态」 |
| **FreePlay** | 约 50% 流量来自 Publishing；Hybrid 游戏占收入 ~30%，LTV 远高于纯 Hyper |
| **JindoBlu** | **双轨**：既有单款（2 Player Games…），也有合集 App |

### 3.2 2026 对小团队的启示

1. **不要追求 App 数量**，追求 **可复用的验证流程**（Rollic 测几百个，上线几个）  
2. 爆款也要 **Hybrid 化**（Meta 层、Daily、Battle Pass），纯 3 天寿命的 Hyper 越来越难  
3. **Portfolio LTV > 单 App 下载量**（FreePlay：Installs 是误导性 KPI）  
4. 第一款成功后，**Cross-Promo 是比 paid UA 更便宜的第二款获客方式**

---

## 4. 单 App 生命周期与 Kill 标准

### 4.1 阶段 gate

| 阶段 | 时长 | 目标 | 通过线（参考，需按品类校准） |
|------|------|------|------------------------------|
| **Prototype** | 1–2 周 | 核心循环有趣 | 内部试玩 + 5–10 人可玩性测试 |
| **CPI Test** | 3–7 天 | 素材 + 玩法匹配 | CPI < 目标上限；CTR 达标 |
| **Soft Launch** | 2–4 周 | 留存 + ARPDAU | D1 ≥25%；D7 ≥5%；ARPDAU ≥$0.03 |
| **Global** | 持续 | ROAS 为正 | D7/D30 ROAS 或 Portfolio 摊薄后盈利 |
| **Kill / Pivot** | — | 止损 | Soft Launch 2 周后 D1<20% 且无改善 → 下架或合入合集 |

### 4.2 单 App 健康 KPI

沿用 [总览文档 §4](./overseas-mini-games-heat-and-retention.md#42-留存基准按品类)：

| 类型 | D1 | D7 | D30 | ARPDAU |
|------|----|----|-----|--------|
| 纯 Hyper | ≥25% | ≥5% | ≥1% | $0.03–$0.08 |
| Hybrid Casual | ≥35% | ≥12% | ≥5% | $0.08–$0.20+ |

---

## 5. 矩阵级基础设施（降本核心）

多款独立 App **必须共享**，否则每款都从零搭 Mediation / Analytics 会拖死产能。

### 5.1 建议共享模块

```
shared-core/
├── mediation/          # AppLovin MAX 统一初始化 + Ad Unit 命名规范
├── analytics/          # Firebase + Tenjin/Adjust 归因
├── cross-promo/        # 互推 UI + 深链 + 频次控制
├── consent/            # GDPR UMP + iOS ATT 流程
├── remote-config/      # 广告频次、Cross-Promo 开关 A/B
└── ui-shell/           # 通用 Pause 菜单、Settings、Rate Us
```

每款游戏 repo 只保留：**核心玩法 + 关卡 + 美术**。

### 5.2 商店与品牌

| 策略 | 说明 |
|------|------|
| **统一 Developer 名** | 如 `YourStudio` 下挂多款，建立认知 |
| **视觉家族感** | Icon 风格、Loading 页统一，降低 Cross-Promo 信任成本 |
| **独立 Bundle ID** | 每 App 必须独立，便于 ASO 和下架隔离 |
| **可选：无品牌合集** | 若某几款表现弱，后期可打包进「XXX Collection」二次利用 |

---

## 6. 交叉推广（Cross-Promotion）

矩阵策略的 **第二根支柱**（第一根是爆款本身）。

### 6.1 为什么必须做

- Paid UA CPI 上涨；自有流量 **CPI ≈ 0**  
- 用户即将 churn 时，导到 **Affinity 更高** 的另一 App → **Portfolio LTV 上升**  
- Voodoo：**Cross-Promo 让团队在 post-ATT 时代仍能识别高价值用户**

### 6.2 放置与频次

|  placement | 适用 | 注意 |
|------------|------|------|
| **Rewarded「试玩我们的新游戏」** | 所有用户 | 用户主动，体验最好 |
| **Interstitial 结束帧** | 非付费、低 LTV 用户 | spender 少推，避免迁移高价值用户 |
| **Pause 菜单「More Games」** | 全量 | JindoBlu / Voodoo 方形入口 |
| **Predictive（Adikteev 等）** | 即将 churn 用户 | 85%+ churn 预测准确率宣称 |

**频次参考**（AppAgent）：

- 非付费用户：Cross-Promo 最多 **~10 次/周**  
- 付费用户：**≤3 次/周**  
- Cross-Promo 与 **第三方广告分开 waterfall**，避免 cannibalization 难衡量  

### 6.3 衡量指标

不看单 App 安装，看 **Portfolio 增量**：

- Cross-Promo 带来的 **Incremental Installs**  
- 源 App 留存/ARPDAU 是否被侵蚀  
- **Portfolio LTV**：用户在多款 App 间的总贡献  

---

## 7. ASO：每 App 独立运营

### 7.1 关键词策略

每 App 抢 **细分词**，而非全家抢 `mini games`：

| 游戏示例 | 目标词方向 |
|----------|------------|
| 双人同屏对战 | `2 player games`, `local multiplayer` |
| 拧螺丝益智 | `screw puzzle`, `sort puzzle` |
| 堆叠跑酷 | `stack runner`, `arcade` |

大词留给 **合集 App** 或 **已验证爆款** 的 Brand Search。

### 7.2 Store 页 = 买量素材的落地页

- 截图 / 视频与 **Meta、TikTok 买量创意** 一致（Playrix、Supercell 做法）  
- 新 Season / 更新 → 同步换 Store 素材，ASO 当 **持续 Conversion 系统** 而非一次性  

---

## 8. 变现（每 App 独立，配置复用）

细节见 [app-store-ad-monetization.md](./app-store-ad-monetization.md)，矩阵补充：

| 点 | 建议 |
|----|------|
| Mediation | 全 App 统一 **AppLovin MAX**，Adapter 版本锁一致 |
| 广告节奏 | Remote Config **按 App、按 cohort** 调 Interstitial 频次 |
| Hybrid | 验证期可加 **去广告 IAP $2.99** 或 **Battle Pass**，拉高 LTV |
| Cross-Promo vs Ads | 高 LTV 用户 waterfall 优先 Cross-Promo，低 LTV 优先 IAA |

---

## 9. 推荐发行节奏（小团队）

假设 2–4 人，Unity 技术栈：

```
Month 1–2   App #1 上线 → Soft Launch → 调留存/广告
Month 2–3   App #2 并行开发；#1 加 Cross-Promo 推 #2
Month 3–4   App #3；复盘 #1 是否 Kill / Hybrid 化
Quarter     目标：3–5 款在架，1 款有正向 ROAS 信号
```

**ponytail 原则**：第一款不要追求完美；追求 **可复制的「壳 + 流程」**；第二款应 **80% 复用代码**。

---

## 10. 风险清单

| 风险 | 应对 |
|------|------|
| 每 App 单独审核 / 下架 | Bundle 隔离；违规 App 不影响矩阵 |
| 维护成本爆炸 | 共享 core；老 App 进入 **maintenance mode**（只修 crash） |
| 无爆款 | 预期内；控制 Soft Launch 预算；快速 Kill |
| Cross-Promo 蚕食源 App 收入 | 分 segment；测 Incrementality |
| 玩法抄袭 | 微创新 + 执行速度；Hybrid 层做差异 |
| 账号关联 | 同一 Developer 账号下多 App 正常；避免 spam 式批量相似 App 被拒 |

---

## 11. 与「聚合 App」的关系（非互斥）

JindoBlu 路径可供参考：

1. **先多 App 矩阵** 验证哪些玩法有量  
2. 把 **表现中等、偏短** 的游戏打包成 **Offline Collection** App，吃 ASO 大词  
3. 爆款 **保持独立**，继续独立买量和品牌  

你们可以 **Phase 1 只做独立 App**；有 5+ 款后再决定是否出合集。

---

## 12. 决策树（选哪种形态）

```
每款游戏是否有独立「一句话卖点」+ 30s 买量素材？
├─ 是 → 独立 App（当前方向）✓
└─ 否 → 是否值得作为合集 filler？
         ├─ 是 → 进聚合 App 或延后
         └─ 否 → Kill

第一款是否已有 D1>30% + 正向 ARPDAU？
├─ 是 → 加 Hybrid 层 + 买量 + Cross-Promo 推新作
└─ 否 → Pivot 核心循环或 Kill（≤4 周 soft launch）
```

---

## 13. 参考资料

| 主题 | 链接 |
|------|------|
| Voodoo Cross-Promo 策略 | https://www.adikteev.com/blog/cross-promotion-for-mobile-app-growth-why-now |
| Cross-Promo 实操指南 | https://appagent.com/blog/a-guide-to-cross-promotion-how-to-increase-installs-for-your-mobile-game-for-free/ |
| Playtika Cross-Promo 分割 waterfall | https://www.deconstructoroffun.com/blog/2021/9/5/secrets-to-successful-cross-promotion |
| SayGames 2025 少而精 | https://www.pocketgamer.biz/saygames-reflects-on-2025-fewer-projects-but-deeper-partnerships/ |
| Rollic Hybrid 策略 | https://www.pocketgamer.biz/how-rollic-scored-a-100m-hybridcasual-hit-by-ideating-1000-games-a-month/ |
| 2026 营销与 ASO | https://stepico.com/blog/mobile-game-marketing-strategy-in-2026/ |
| IAA / Mediation | [app-store-ad-monetization.md](./app-store-ad-monetization.md) |
