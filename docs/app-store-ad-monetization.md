# App 商店上架 + 广告聚合变现调研

> **适用场景**：每个独立小游戏 App 的 IAA 变现（亦适用于未来可能的合集 App）  
> **产品方向**：多款小游戏各自独立 App → [多 App 矩阵策略](./multi-app-portfolio-strategy.md)  
> **面向市场**：海外用户  
> **关联文档**：[热度与粘性总览](./overseas-mini-games-heat-and-retention.md)

---

## 1. 结论摘要

| 维度 | 判断 |
|------|------|
| **模式可行性** | ✅ 已验证。单 App 超休闲/Hybrid 是海外主流；矩阵靠 **1–2 款爆款 + Cross-Promo** |
| **收入公式** | 单 App：**LTV ≈ ARPDAU × 留存天数**；矩阵：**Portfolio LTV**（用户在多款 App 间总贡献） |
| ** mediation 选型** | 海外首选 **AppLovin MAX**；全 App **共享同一套 SDK 配置** |
| **与聚合 App 差异** | 独立 App 靠 **细分 ASO + 买量素材**；Imp/DAU 来自单游戏内断点，非换游戏 |
| **矩阵必做** | **Cross-Promotion**：把即将流失用户导到下一款；CPI 接近 0 |

---

## 2. 商业模式拆解

### 2.1 收入链路

```
用户安装 App
    → 浏览/启动多款小游戏（聚合价值）
    → 产生广告展示（Banner / Interstitial / Rewarded / App Open）
    → Mediation 竞价选出最高出价 Network
    → 开发者获得 eCPM 分成
```

**纯 IAA 聚合 App 没有 IAP 时，Google/Apple 的 30% 抽成不适用广告收入**（仅 IAP/订阅抽成）。

### 2.2 关键公式

| 指标 | 公式 | 说明 |
|------|------|------|
| **ARPDAU** | 日广告总收入 ÷ DAU | **最重要**变现指标 |
| **Imp/DAU** | 日展示次数 ÷ DAU | 聚合 App 天然优势：换游戏 = 新插屏点位 |
| **eCPM** | 收入 ÷ 展示 × 1000 | 随地区/格式波动，勿单独优化 |
| **LTV（IAA）** | ARPDAU × 平均活跃天数 | 买量 ROI 基准 |
| **ROAS** | LTV ÷ CPI | CPI 需 < LTV 才可持续买量 |

**超休闲 IAA 参考 ARPDAU**：$0.03–$0.08（Tier 1 可更高；东南亚 Tier 3 显著更低）。

### 2.3 聚合 App 的变现优势

相比单款超休闲：

| 优势 | 机制 |
|------|------|
| **更多插屏触点** | 游戏切换、返回大厅、关卡结束均可展示 |
| **更长单次 Session** | 用户连续试多款游戏 → 总 Imp 上升 |
| **Rewarded 场景多** | 「看广告解锁新游戏 / 提示 / 复活」 |
| **降低单游戏疲劳** | 内容多样性支撑 D7，间接拉高 LTV |

---

## 3. 商店竞品参考

### 3.1 头部标杆

| App | 下载量 | 特点 |
|-----|--------|------|
| **Offline Games**（JindoBlu） | **100M+** | 20+ 真实小游戏；强调离线；Google Play #2 免费 Casual |
| **2 3 4 Player Mini Games**（JindoBlu 系） | 50M+ 量级 | 多人同屏，社交场景 |
| **Mini Games Offline All in One** | 1M+ | 2048、Water Sort 等益智合集；「100+ games」营销 |
| **各类「1000 Offline Games」** | 不等 | 多为 **20–40 款重复包装** + 高频广告；SEO 导向 |

### 3.2 市面问题（差异化机会）

低质聚合 App 常见做法（应避免或改进）：

- 标题夸大游戏数量，实际大量重复换皮  
- 每 **90–120 秒** 强制插屏 → 差评与卸载  
- 声称离线但仍请求网络（仅为广告/analytics）  
- 无跨游戏进度 / 账号体系  

**你们的机会**：用 **真实策展 + 可控广告频次 + 平台级进度** 做精品聚合，而非堆量壳 App。

---

## 4. 广告聚合（Mediation）方案

### 4.1 平台选型（2025–2026 海外）

| Mediation | 市占/定位 | 适合场景 |
|-----------|-----------|----------|
| **AppLovin MAX** | Top 下载游戏中 ~**73%** 使用；Rewarded eCPM Tier 1 常领先 | **超休闲 / 休闲 IAA 首选** |
| **Unity LevelPlay** | Top 收入游戏中 ~25%；ironSource 底子 | Unity 技术栈、Android 部分市场 |
| **Google AdMob** | 稳定、覆盖广；eCPM 常居中 | 备份 Network + 部分 Android 主力 |
| **CAS（Clever Ads Solutions）** | 轻量、有 Tenjin 基准数据 | 中小团队快速接入 |

> 2026 年主流已是 **In-App Bidding（竞价）**；纯 Waterfall 会损失约 **15%–25%** 收入。MAX 于 2025.07 起强制 bidding-only。

### 4.2 建议接入的 Ad Network

| Network | 强项 | 备注 |
|---------|------|------|
| **AppLovin** | Rewarded、Tier 1 | MAX 自家 demand |
| **Google AdMob** | 全球 fill、Banner | 必接 |
| **Meta Audience Network** | 部分市场 eCPM 高 | iOS 受 ATT 影响 |
| **Unity Ads** | 游戏流量 | LevelPlay 深度整合 |
| **Mintegral** | Android、亚洲 | Tenjin：Android 份额 ~17% |
| **Pangle（TikTok）** | 部分海外市场 | 需合规评估 |
| **Liftoff / AdColony** | 视频质量 | 作补充 demand |

### 4.3 广告格式与放置建议（聚合 App）

| 格式 | eCPM 相对 | 推荐场景 | 频次建议 |
|------|-----------|----------|----------|
| **Rewarded Video** | 最高 | 解锁游戏、额外生命、双倍奖励 | 用户主动；无硬上限 |
| **Interstitial** | 中高 | **游戏结束**、**返回大厅**、每 N 局 | 避免 <90s 强插；D1 用户更保守 |
| **App Open** | 中 | 冷启动 / 从后台恢复 | 每日首次即可，忌每次恢复 |
| **Banner / MREC** | 低 | 游戏选择大厅底部 | 常驻但占屏面积受控 |
| **Native** | 中 | 游戏列表「推荐位」 | 需明确标注 Ad |

**原则**：Interstitial 是 Imp/DAU 主力，但 **频次与留存负相关**；用 cohort 找 ARPDAU × Retention 最优平衡点。

### 4.4 eCPM 与地区（参考区间）

> 来源：Tenjin + CAS Q1–Q2 2024 等行业报告。实际随季节、品类、ATT 状态波动。

| 格式 | Tier 1（美/英/德） | Tier 2（东南亚等） |
|------|-------------------|-------------------|
| Rewarded | ~$15–$35+ | ~$3–$10 |
| Interstitial | ~$8–$20 | ~$2–$6 |
| Banner | ~$0.5–$2 | ~$0.1–$0.5 |

**Network 份额参考（Tenjin）**：

- iOS 广告收入：AppLovin ~39%，Mintegral ~21%  
- Android 广告收入：AdMob ~22%，Mintegral ~17%，AppLovin ~17%

---

## 5. App 模式下的热度与粘性

### 5.1 相对 Web 聚合的变化

| 维度 | Web（Poki 类） | App 商店聚合 |
|------|----------------|--------------|
| 获客 | SEO、自然链接 | **ASO**、Google UAC、Meta、TikTok 买量 |
| 首访成本 | 极低（点击即玩） | 安装转化漏斗（Store Page → Install） |
| 留存工具 | 弱（Web Push 权限低） | **Push、本地通知、Daily Reward** |
| 粘性预期 | 平台 DAU/MAU ~12%–18% | 精品聚合可瞄准 **15%–22%** |
| 变现 | 页面广告 | SDK 级 Mediation，eCPM 通常 **高于 Mobile Web** |

### 5.2 留存基准（Native 超休闲 / 休闲合集）

沿用 [总览文档 §4.2](./overseas-mini-games-heat-and-retention.md#42-留存基准按品类)，App 壳 + 多款小游戏按 **平台级** 衡量：

| 指标 | 目标（起步 → 健康） | 备注 |
|------|---------------------|------|
| **D1** | 28% → 35%+ | 首屏游戏选择 + 首局 60s 内正反馈 |
| **D7** | 6% → 12% | Daily Reward + Continue Playing |
| **D30** | 2% → 5% | 合集 App 通常优于单款超休闲 |
| **DAU/MAU** | 12% → 20% | Push + Daily Quest 驱动 |
| **Sessions/DAU** | 1.5 → 2.5+ | 每多 1 Session ≈ 多 1–2 次广告机会 |
| **Imp/DAU** | 5 → 12+ | 聚合 App 核心杠杆 |

### 5.3 提升 LTV 的系统设计（IAA 导向）

优先级排序：

1. **大厅 → 游戏 → 大厅** 闭环顺畅（减少加载放弃）  
2. **Interstitial 仅在自然断点**（局末/切换），D1 cohort 单独降频 A/B  
3. **Rewarded 换价值**（解锁热门游戏、去广告 30min）  
4. **Daily：玩 3 款不同游戏领奖励** → 拉高 Imp/DAU 与 DAU/MAU  
5. **Push**：「今日新游」「好友分数被超越」行为触发  
6. **去广告 IAP（可选）**：$2.99–$4.99 一次性；不抢 IAA 主力，但改善评分  

---

## 6. 获客与 ASO（海外）

### 6.1 关键词方向

Store 上高流量词（竞品在用）：

- `offline games` / `no wifi games`  
- `mini games` / `mini games offline`  
- `2 player games` / `puzzle games`  
- `all in one games` / `game collection`

注意：「1000 games」类词带来流量也带来 **低质预期与高卸载**；若游戏数真实较少，不建议夸大。

### 6.2 买量（若预算允许）

| 渠道 | 适用 | 参考 |
|------|------|------|
| **Google UAC** | Android 主力 | 休闲类 CPI Tier 1 约 $1–$3+ |
| **Meta App Ads** | iOS/Android | 需创意短视频展示多款游戏 |
| **TikTok** | 年轻市场 | 玩法 clip 易展示合集价值 |
| **AppLovin / Unity Ads** | ROAS _campaign | MAX 发布商可对接 AppLovin UA |

**盈亏平衡**：`CPI < ARPDAU × D7_LTV_multiplier`；IAA 产品通常看 **D0/D1 ROAS**，超休闲案例 D1 ROAS 100%+ 才可持续放量（需自家数据校准）。

---

## 7. 平台政策与合规

| 风险 | 说明 | 应对 |
|------|------|------|
| **广告过多** | Google / Apple 均要求广告不能破坏体验；频繁插屏导致拒审或下架 | 审核版降低频次；分 cohort 控制 |
| **儿童用户** | COPPA / Google Families Policy；儿童向需专用 SDK、禁行为广告 | 若目标全年龄，避免 13- 以下定向 |
| **iOS ATT** | IDFA  opt-in 低 → iOS eCPM 低于 Android | 做好 SKAN / AEM；Android 可先验证模型 |
| **GDPR / CCPA** | 欧盟/加州需 CMP  consent | 接入 UMP（Google）或同类 CMP |
| **游戏版权** | 聚合第三方 Web 游戏存在 IP 风险 | 自制 / 授权 / SDK 接入正版内容 |
| **误导性描述** | 「1000 games」与实际不符 → 差评与政策风险 | Store 描述与 App 内一致 |

---

## 8. 推荐 KPI 仪表盘（App + IAA）

### 8.1 每日必看

```
获客：Installs | Store CVR | CPI（若有买量）
活跃：DAU | Sessions/DAU | 平均 Session 时长
留存：D1/D7/D30（按渠道/国家 cohort）
变现：ARPDAU | Imp/DAU | eCPM（分格式）| Fill Rate
质量：Crash Rate | ANR | 1-star 评论率
```

### 8.2 健康线（IAA 聚合 App，海外）

| 指标 | 红线 | 健康 |
|------|------|------|
| ARPDAU | <$0.02 | $0.05+（Tier 1 混合流量） |
| Imp/DAU | <4 | 8+ |
| D1 留存 | <22% | 30%+ |
| Sessions/DAU | <1.2 | 2.0+ |
| Crash Rate | >1% | <0.5% |

### 8.3 Mediation 实验清单

- [ ] MAX vs LevelPlay 50/50 分流量 4–6 周，比 **ARPDAU**  
- [ ] Interstitial 频次：每 1 局 vs 每 2 局 vs 仅换游戏  
- [ ] App Open：开 vs 关对 D1 影响  
- [ ] Rewarded 解锁游戏：参与率 vs 总 ARPDAU  
- [ ] Banner 大厅：开 vs 关对 Session 长度影响  

---

## 9. 技术实现要点（简）

| 模块 | 建议 |
|------|------|
| **游戏容器** | Unity 主壳 + 多款小游戏；或 WebView/HTML5 子游戏（注意性能） |
| **Mediation SDK** | AppLovin MAX 为主 SDK；各 Network Adapter 按需加 |
| **Analytics** | GameAnalytics / Firebase + Tenjin 或 Adjust（归因） |
| **A/B** | Firebase Remote Config 或 MAX 内置实验 |
| **广告 consent** | Google UMP + iOS ATT 弹窗时机 A/B |

---

## 10. 与 Web 方案对比（决策参考）

| | **App 商店 + IAA（当前方向）** | **Web 聚合（Poki 模式）** |
|--|-------------------------------|---------------------------|
| 启动成本 | 中（壳 App + SDK + 审核） | 高（SEO、品牌、开发者生态） |
| 获客 | 买量 + ASO | SEO 为主 |
| 变现 ceiling | Mediation 成熟，ARPDAU 可预期 | 页面广告 eCPM 通常更低 |
| 留存 | Push + Daily 系统 | 依赖回访与书签 |
| 竞争 | 壳 App 红海，需差异化 | Poki/CrazyGames 头部垄断 |
| 长期壁垒 | 内容 + 体验 + 数据 | 品牌 + SEO + 开发者关系 |

**Lazy 建议（ponytail）**：若团队暂无 SEO/Web 运营能力，**App + MAX 是更快验证 IAA 的路径**；先靠 10–20 款高质量小游戏 + 合理广告节奏跑通 `ARPDAU > CPI`，再考虑 Web 版导量或 PWA。

---

## 11. 参考资料

| 主题 | 链接 |
|------|------|
| Tenjin 广告变现基准 2025/2026 | https://tenjin.com/blog/ad-mon-gaming-2025/ |
| Google AdMob 游戏变现指南 | https://admob.google.com/home/resources/monetize-mobile-game-with-ads/ |
| AppLovin MAX vs LevelPlay 对比 | https://monetizationguy.com/articles/applovin-max-vs-unity-levelplay |
| JindoBlu Offline Games（竞品） | https://play.google.com/store/apps/details?id=com.JindoBlu.OfflineGames |
| Hybrid Casual 市场概览 | https://lancaric.substack.com/p/2025-hybridcasual-market-overview |
| 低质「1000 games」App 分析 | https://electronics.alibaba.com/question/1000-offline-games-truths,-risks-real-world-use |
