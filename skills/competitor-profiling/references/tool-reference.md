# 竞品分析 MCP 工具参考

竞品分析中使用的 Firecrawl 和 DataForSEO MCP 工具的快速参考。

## 目录
- Firecrawl 工具（网站抓取）
- DataForSEO 工具（SEO 与市场数据）
- 推荐执行顺序
- 错误处理

---

## Firecrawl 工具

### firecrawl_map
**用途**: 发现竞争对手网站上的所有 URL，以识别关键页面。
**使用时机**: 每个竞争对手的第一步——在抓取单个页面之前。
**关键输出**: URL 列表及其页面类型/路径。
**提示**: 查找包含 `/pricing`、`/features`、`/about`、`/customers`、`/integrations`、`/blog`、`/changelog` 的路径。

### firecrawl_scrape
**用途**: 将单个页面的内容提取为干净的 markdown。
**使用时机**: 映射完成后，逐个抓取每个关键页面。
**关键输出**: markdown 格式的页面内容——标题、正文文本、结构化数据。
**提示**: 首先抓取首页——它可以一次性揭示定位、受众和社会证明。

### firecrawl_search
**用途**: 搜索网络上关于竞争对手的特定内容。
**使用时机**: 查找不在其自己网站上的评论页面、新闻报道或竞争对手提及。
**示例查询**:
- `"[Competitor Name]" site:g2.com`
- `"[Competitor Name]" review`
- `"[Competitor Name]" funding OR raised`

### firecrawl_crawl
**用途**: 在一次操作中抓取网站中的多个页面。
**使用时机**: 需要分析许多页面的深度档案（例如，所有功能页面、所有博客文章）。成本较高——有选择地使用。
**提示**: 设置页面限制以避免抓取整个网站。针对特定的 URL 模式。

### firecrawl_extract
**用途**: 使用架构从页面中提取结构化数据。
**使用时机**: 当你需要以一致格式获取特定数据点时（例如，定价层级详情、功能列表）。
**提示**: 为你想要提取的内容定义清晰的架构——比解析原始 markdown 更可靠。

---

## DataForSEO MCP 工具

### 域名级智能

#### backlinks_summary
**用途**: 获取域名权威度、总反向链接数、引用域名数、垃圾邮件评分。
**输入**: 目标域名（例如 `competitor.com`）
**关键指标**: `domain_rank`、`total_backlinks`、`referring_domains`、`backlinks_spam_score`

#### backlinks_referring_domains
**用途**: 列出顶级引用域名——显示其链接权重的来源。
**输入**: 目标域名 + 限制数量
**关键指标**: 每个域名的: `rank`、`backlinks`、`domain` 名称

#### dataforseo_labs_google_domain_rank_overview
**用途**: 自然搜索概览——流量、关键词、流量价值。
**输入**: 目标域名
**关键指标**: `organic_count`（关键词）、`organic_traffic`（预估每月）、`organic_cost`（流量价值，美元）

#### dataforseo_labs_google_ranked_keywords
**用途**: 域名排名的关键词及其位置。
**输入**: 目标域名
**关键指标**: 每个关键词: `keyword`、`position`、`search_volume`、`url`（排名页面）
**提示**: 按流量排序以找到他们最有价值的关键词。

#### dataforseo_labs_google_keywords_for_site
**用途**: 与域名相关的关键词——比排名关键词更广泛，包括机会。
**输入**: 目标域名
**关键指标**: `keyword`、`search_volume`、`competition`、`cpc`

### 竞争分析

#### dataforseo_labs_google_competitors_domain
**用途**: 通过关键词重叠找到域名的最接近的自然搜索竞争对手。
**输入**: 目标域名
**关键指标**: `domain`、`avg_position`、`intersections`（共享关键词）、`full_domain_rank`
**提示**: 可能会揭示用户未曾考虑过的竞争对手。

#### dataforseo_labs_google_domain_intersection
**用途**: 找到两个域名都排名的关键词——显示直接竞争。
**输入**: 两个目标域名
**关键指标**: `keyword`、每个域名的位置、`search_volume`
**提示**: 用此来比较用户的域名与每个竞争对手。

#### dataforseo_labs_google_relevant_pages
**用途**: 根据自然流量找到域名最重要的页面。
**输入**: 目标域名
**关键指标**: `page`、`metrics`（每页的流量、关键词）
**提示**: 揭示其内容策略——哪些页面驱动最多的价值。

### 技术检测

#### domain_analytics_technologies_domain_technologies
**用途**: 检测域名使用的技术栈。
**输入**: 目标域名
**关键指标**: 按类别分组的技术（CMS、分析、营销、支付等）

### 反向链接深入分析

#### backlinks_backlinks
**用途**: 列出指向域名的单个反向链接。
**输入**: 目标域名 + 限制数量
**关键指标**: `url_from`、`url_to`、`anchor`、`domain_from_rank`、`is_new`

#### backlinks_bulk_ranks
**用途**: 一次性比较多个域名的域名排名。
**输入**: 目标域名数组
**关键指标**: 每个域名的 `domain_rank`
**提示**: 用于总结对比表。

---

## 推荐执行顺序

### 快速扫描（每个竞争对手）

```
1. firecrawl_map → 获取网站 URL
2. 并行执行:
   a. firecrawl_scrape → 首页
   b. firecrawl_scrape → 定价页面
   c. dataforseo_labs_google_domain_rank_overview → 自然搜索指标
   d. backlinks_summary → 域名权威度
3. 综合成简化档案
```

### 深度档案（每个竞争对手）

```
1. firecrawl_map → 获取网站 URL
2. 并行执行（批次 1 — 抓取）:
   a. firecrawl_scrape → 首页
   b. firecrawl_scrape → 定价页面
   c. firecrawl_scrape → 功能页面
   d. firecrawl_scrape → 关于页面
   e. firecrawl_scrape → 客户/案例研究页面
   f. firecrawl_scrape → 集成页面
3. 并行执行（批次 2 — SEO 数据）:
   a. dataforseo_labs_google_domain_rank_overview
   b. dataforseo_labs_google_ranked_keywords
   c. backlinks_summary
   d. backlinks_referring_domains
   e. dataforseo_labs_google_relevant_pages
   f. dataforseo_labs_google_competitors_domain
4. 并行执行（批次 3 — 可选额外项）:
   a. domain_analytics_technologies_domain_technologies
   b. firecrawl_search → G2/Capterra 评论
   c. dataforseo_labs_google_domain_intersection（与用户域名对比）
5. 综合成完整档案
```

### 多竞争对手（3+ 竞争对手）

```
1. 并行映射所有竞争对手网站
2. 并行抓取所有首页，然后并行抓取所有定价页面
3. 并行拉取所有域名的 domain_rank_overview
4. 一次性拉取所有域名的 backlinks_bulk_ranks
5. 按顺序构建档案（综合需要专注）
6. 最后构建总结对比
```

---

## 错误处理

| 问题 | 操作 |
|-------|--------|
| Firecrawl 抓取返回空/被阻止 | 尝试使用 `firecrawl_browser_create` 处理 JS 密集型网站 |
| 在地图中未找到定价页面 | 搜索 `/pricing`、`/plans`、`/packages` —— 某些网站使用不同的路径 |
| DataForSEO 返回域名的无数据 | 域名可能太新或太小——在档案中标注"数据不足" |
| 达到速率限制 | 分散请求；优先处理最高价值的数据 |
| 评论页面抓取被阻止 | 使用 `firecrawl_search` 查找缓存或替代评论来源 |
