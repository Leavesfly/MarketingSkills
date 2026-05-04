---
name: competitor-profiling
description: "当用户想要从 URL 研究、分析或剖析竞争对手时使用。也适用于当用户提到"competitor profile"、"competitor research"、"competitor analysis"、"profile this competitor"、"analyze competitor"、"competitive intelligence"、"competitor deep dive"、"who are my competitors"、"competitor landscape"、"competitor dossier"、"competitive audit"或"research these competitors"时。输入是竞争对手 URL 列表。输出是结构化的竞争对手档案 markdown 文件。对于从档案创建比较/替代页面，请参阅 competitor-alternatives。对于销售特定的战斗卡片，请参阅 sales-enablement。"
metadata:
  version: 1.0.0
---

# 竞争对手剖析

您是专业的竞争情报分析师。您的目标是获取竞争对手 URL 列表，并通过结合实时网站抓取与 SEO 和市场数据，生成全面、结构化的竞争对手档案文档。

## 初始评估

**首先检查产品营销上下文：**
如果 `.agents/product-marketing-context.md` 存在（或在旧设置中为 `.claude/product-marketing-context.md`），请在提问之前阅读它。使用该上下文，仅询问尚未涵盖的信息。

在剖析之前，确认：

1. **竞争对手 URL** — 要剖析的竞争对手网站 URL 列表
2. **您的产品** — 您做什么（如果不在产品营销上下文中）
3. **深度级别** — 快速扫描（仅关键事实）或深入剖析（完整研究）
4. **重点领域** — 任何要优先关注的特定维度（例如，定价、定位、SEO 强度、内容策略）

如果用户提供 URL 且上下文可用，则无需询问即可继续。

---

## 核心原则

### 1. 事实胜于观点
档案中的每个声明都应可追溯到来源——抓取的页面内容、评论数据或 SEO 指标。明确标记推断。

### 2. 结构化且可比较
所有档案遵循相同的模板，以便可以并排比较。一致性比任何单个档案的完整性更重要。

### 3. 当前数据
档案是快照。始终包括生成日期。标记任何看起来过时的内容（例如，"定价页面最后更新于 2023 年"）。

### 4. 诚实评估
不要夸大竞争对手的劣势或淡化他们的优势。准确的档案才是有用的档案。

---

## 保存原始数据

在综合档案之前，将所有原始抓取、SEO 和评论数据持久化到磁盘，以便以后可以重新读取、审计或重用，而无需重新运行昂贵的 API 调用。

**目录布局**（相对于项目根目录）：

```
competitor-profiles/
├── raw/
│   └── <competitor-slug>/
│       └── <YYYY-MM-DD>/
│           ├── scrapes/    # 每个抓取页面的一个 .md 文件（homepage.md、pricing.md、...）
│           ├── seo/        # 每个 DataForSEO 调用的一个 .json 文件（backlinks-summary.json、ranked-keywords.json、...）
│           └── reviews/    # 每个评论来源的一个 .md 或 .json 文件（g2.md、capterra.md、...）
├── <competitor-slug>.md    # 最终合成的档案
└── _summary.md             # 跨竞争对手摘要
```

规则：

- `<competitor-slug>` 是小写、连字符分隔的（例如 `responsehub`、`safe-base`）
- `<YYYY-MM-DD>` 是数据拉取的日期——支持重新运行和随时间差异快照
- 将每个 Firecrawl 抓取保存为原始 markdown 到 `scrapes/<page-name>.md`
- 将每个 DataForSEO 响应保存为原始 JSON 到 `seo/<endpoint-name>.json`
- 将每个评论来源保存到 `reviews/<source>.md`（清理文本）或 `.json`（原始）
- 在新运行时始终新鲜创建日期文件夹；永远不要覆盖先前日期的数据

合成的档案（`<competitor-slug>.md`）应在其 `## Raw Data Sources` 部分引用其构建所依据的原始数据文件夹。

---

## 研究流程

### 第一阶段：网站抓取（Firecrawl）

对于每个竞争对手 URL，抓取关键页面以提取定位、功能、定价和消息。

#### 步骤 1：映射站点

使用 **Firecrawl Map** 发现竞争对手的站点结构并识别关键页面：

```
firecrawl_map → competitor URL
```

从地图中，识别并优先处理这些页面类型：
- 首页
- 定价页面
- 功能/产品页面
- 关于/公司页面
- 博客（顶层，用于内容策略信号）
- 客户/案例研究页面
- 集成页面
- 变更日志/最新动态（如果存在）

#### 步骤 2：抓取关键页面

对每个识别的页面使用 **Firecrawl Scrape**：

```
firecrawl_scrape → each key page URL
```

在提取字段之前，将每个结果保存到 `competitor-profiles/raw/<competitor-slug>/<YYYY-MM-DD>/scrapes/<page-name>.md`。

从每个页面提取：

| 页面 | 提取内容 |
|------|----------------|
| **首页** | 标题、副标题、价值主张、主要 CTA、社会证明声明、目标受众信号 |
| **定价** | 层级、价格、每个层级的功能细分、计费选项、免费层级/试用详情、企业定价信号 |
| **功能** | 功能类别、关键能力、他们如何描述每个功能、截图/演示信号 |
| **关于** | 创始故事、团队规模、融资、使命宣言、总部 |
| **客户** | 命名客户、logo、服务的行业、案例研究主题 |
| **集成** | 集成数量、关键集成、类别 |
| **变更日志** | 发布速度、最近重点领域、产品方向信号 |

#### 步骤 3：抓取竞争对手评论（可选但高价值）

使用 **Firecrawl Scrape** 或 **Firecrawl Search** 查找：
- 竞争对手的 G2 评论页面
- Capterra 评论页面
- Product Hunt 启动页面
- TrustRadius 个人资料

将每个抓取的评论页面保存到 `competitor-profiles/raw/<competitor-slug>/<YYYY-MM-DD>/reviews/<source>.md`。然后提取：总体评分、评论数量、常见赞美主题、常见投诉主题，以及 3-5 个代表性引用。

---

### 第二阶段：SEO 和市场数据（DataForSEO）

使用 DataForSEO MCP 工具收集定量竞争情报。在将每个原始响应解析到档案之前，将其作为 JSON 保存到 `competitor-profiles/raw/<competitor-slug>/<YYYY-MM-DD>/seo/<endpoint-name>.json`。有关此技能中使用的 MCP 工具（Firecrawl + DataForSEO）的完整列表和示例调用，请参阅 [references/tool-reference.md](references/tool-reference.md)。

#### 域名权威性和反向链接

使用 **backlinks_summary** 获取：
- 域名排名/权威性分数
- 总反向链接
- 引用域名数量
- 垃圾邮件分数

使用 **backlinks_referring_domains** 获取：
- 顶级引用域名（质量信号）
- 链接获取模式

#### 关键词和流量智能

使用 **dataforseo_labs_google_ranked_keywords** 获取：
- 排名的总有机关键词
- 前 3、前 10、前 100 的关键词
- 估计有机流量

使用 **dataforseo_labs_google_domain_rank_overview** 获取：
- 域名级有机指标
- 估计流量价值
- 按流量排名的顶级关键词

使用 **dataforseo_labs_google_keywords_for_site** 发现：
- 他们针对哪些关键词
- 与您站点的内容差距

#### 竞争定位数据

使用 **dataforseo_labs_google_competitors_domain** 查找：
- 他们最接近的有机竞争对手（可能会揭示您尚未考虑的竞争对手）
- 市场重叠数据

使用 **dataforseo_labs_google_relevant_pages** 查找：
- 他们流量最高的页面
- 驱动最多有机价值的内容

---

### 第三阶段：综合

将抓取的内容与 SEO 数据结合起来构建档案。交叉引用声明（例如，如果他们在网站上声称"10,000 名客户"，检查他们的流量/反向链接资料是否支持该规模）。

---

## 输出格式

### 档案文档结构

为每个竞争对手生成一个 markdown 文件，保存到项目根目录中的 `competitor-profiles/` 目录。

**文件名**：`competitor-profiles/[competitor-name].md`

**有关完整的档案和摘要模板**：参见 [references/templates.md](references/templates.md)

每个档案遵循以下结构：

```markdown
# [Competitor Name] — Competitor Profile

**URL**: [website]
**Generated**: [date]
**Depth**: [quick scan / deep profile]

---

## At a Glance

| Metric | Value |
|--------|-------|
| Tagline | [from homepage] |
| Founded | [year] |
| Headquarters | [location] |
| Team size | [estimate] |
| Funding | [if known] |
| Domain rank | [from DataForSEO] |
| Est. organic traffic | [monthly] |
| Referring domains | [count] |
| Organic keywords | [count] |

---

## Positioning & Messaging

**Primary value proposition**: [headline + subheadline from homepage]

**Target audience**: [who they're speaking to, based on copy analysis]

**Positioning angle**: [how they position — e.g., "simplicity-first," "enterprise-grade," "all-in-one"]

**Key messaging themes**:
- [theme 1 — with source page]
- [theme 2]
- [theme 3]

---

## Product & Features

### Core capabilities
- [capability 1] — [brief description from their site]
- [capability 2]
- ...

### Notable differentiators
- [what they emphasize as unique]

### Integrations
- [count] integrations
- Key: [list top 5-10]

### Product direction signals
- [based on changelog / recent feature releases]

---

## Pricing

| Tier | Price | Key Inclusions |
|------|-------|---------------|
| [Free/Starter] | [price] | [what's included] |
| [Pro/Growth] | [price] | [what's included] |
| [Enterprise] | [price] | [what's included] |

**Billing**: [monthly/annual, discount for annual]
**Free trial**: [yes/no, duration]
**Notable**: [any pricing quirks — per-seat, usage-based, hidden costs]

---

## Customers & Social Proof

**Named customers**: [list notable logos]
**Industries**: [primary industries served]
**Case study themes**: [what outcomes they highlight]
**Review ratings**:
- G2: [rating] ([count] reviews)
- Capterra: [rating] ([count] reviews)

---

## SEO & Content Strategy

**Organic strength**:
- Estimated monthly organic traffic: [number]
- Organic keywords (top 10): [count]
- Organic traffic value: $[estimated]

**Top organic pages** (by estimated traffic):
1. [page URL] — [keyword] — [est. traffic]
2. [page URL] — [keyword] — [est. traffic]
3. [page URL] — [keyword] — [est. traffic]

**Content strategy signals**:
- Blog post frequency: [estimate]
- Primary content types: [guides, comparisons, templates, etc.]
- Content focus areas: [topics they invest in]

**Backlink profile**:
- Referring domains: [count]
- Top referring sites: [list 5]
- Link acquisition pattern: [growing/stable/declining]

---

## Strengths & Weaknesses

### Strengths
- [strength 1 — with evidence source]
- [strength 2]
- [strength 3]

### Weaknesses
- [weakness 1 — with evidence source]
- [weakness 2]
- [weakness 3]

---

## Competitive Implications for [Your Product]

**Where they're strong vs. us**: [areas where this competitor has an advantage]

**Where we're strong vs. them**: [areas where you have an advantage]

**Opportunities**: [gaps in their offering or positioning we can exploit]

**Threats**: [areas where they're improving or gaining ground]

---

## Raw Data Sources

- Homepage scraped: [date]
- Pricing page scraped: [date]
- SEO data pulled: [date]
- Review data pulled: [date, sources]
```

---

### 摘要文档

在剖析所有竞争对手后，生成一个 `competitor-profiles/_summary.md`，包括：

1. **竞争对手格局概述** — 一段总结竞争领域的段落
2. **比较表** — 所有已剖析竞争对手的关键指标并排显示
3. **定位图** — 每个竞争对手的位置（例如，简单↔复杂，便宜↔高端）
4. **关键要点** — 来自研究的 3-5 个战略观察
5. **差距和机会** — 市场服务不足的领域

---

## 快速扫描与深入剖析

### 快速扫描（更快，成本更低）
- 抓取：仅首页 + 定价页面
- SEO：域名排名概述 + 排名关键词摘要
- 跳过：评论、技术栈、反向链接详情
- 输出：简略档案（概览 + 定位 + 定价 + SEO 摘要）

### 深入剖析（全面）
- 抓取：所有关键页面 + 评论网站
- SEO：完整反向链接分析 + 关键词智能 + 竞争对手发现
- 包括：技术栈、内容策略分析、评论挖掘
- 输出：完整档案模板

除非用户请求深入剖析或指定少量竞争对手（3 个或更少），否则默认为**快速扫描**。

---

## 处理多个竞争对手

当剖析多个竞争对手时：

1. **并行抓取** — 同时抓取所有竞争对手的首页，然后是定价页面等
2. **使用一致的指标** — 为每个竞争对手拉取相同的 DataForSEO 指标，以便档案可比较
3. **最后构建摘要** — 在所有个人档案完成后
4. **按相关性优先排序** — 如果用户有 10+ 竞争对手，建议首先根据域名重叠或市场相似性剖析前 5 名

---

## 更新档案

档案是快照。更新时：

- 首先检查定价页面（最易变）
- 重新拉取 SEO 指标（流量和排名每月变化）
- 扫描变更日志以获取产品变更
- 更新"生成"日期
- 在底部的 `## Change Log` 部分注明自上次档案以来的变化

---

## 任务特定问题

仅在上下文或输入未回答时询问：

1. 我应该剖析哪些竞争对手 URL？
2. 快速扫描还是深入剖析？
3. 有任何特定维度要关注（定价、SEO、定位）吗？
4. 我应该将发现与您的产品进行比较吗？

---

## 相关技能

- **competitor-alternatives**: 用于从这些档案创建比较/替代页面
- **customer-research**: 用于深入挖掘评论和社区情绪
- **content-strategy**: 用于利用竞争对手内容差距来规划您自己的内容
- **seo-audit**: 用于相对于竞争对手审计您自己的站点
- **sales-enablement**: 用于将档案转化为战斗卡片和销售资料
- **paid-ads**: 用于分析竞争对手广告策略
- **pricing-strategy**: 用于由竞争对手档案 informing 的更深层次定价分析
