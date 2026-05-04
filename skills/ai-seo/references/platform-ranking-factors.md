# 每个 AI 平台如何选择来源

每个 AI 搜索平台都有自己的搜索索引、排名逻辑和内容偏好。本指南涵盖在每个平台上获得引用所需了解的内容。

文中引用的来源：普林斯顿 GEO 研究（KDD 2024）、SE Ranking 域名权威度研究、ZipTie 内容-答案匹配分析。

---

## 基础要素

每个 AI 平台都有三个基本要求：

1. **你的内容必须在其索引中** — 每个平台使用不同的搜索后端（Google、Bing、Brave 或它们自己的）。如果你未被索引，你就无法被引用。
2. **你的内容必须可爬取** — AI 机器人需要通过 robots.txt 访问。阻止机器人，就会失去引用。
3. **你的内容必须可提取** — AI 系统提取的是段落，而不是页面。清晰的结构和自包含的段落胜出。

除了这些基础知识外，每个平台对不同信号的权重不同。以下是重要因素及其适用平台。

---

## Google AI Overviews

Google AI Overviews 从 Google 自己的索引中提取内容，并高度依赖 E-E-A-T 信号（经验、专业知识、权威性、可信度）。它们出现在约 45% 的 Google 搜索中。

**Google AI Overviews 的不同之处：** 它们已经拥有你的传统 SEO 信号——反向链接、页面权威度、主题相关性。额外的 AI 层增加了对带有引用来源和结构化数据的内容的偏好。研究表明，在内容中包含权威引用与 132% 的可见性提升相关，而以权威（而非销售）语气写作再增加 89%。

**重要的是，AI Overviews 不仅仅重复传统的 Top 10。** 只有约 15% 的 AI Overview 来源与传统有机结果重叠。在传统搜索中无法进入第一页的页面，如果具有强大的结构化数据和清晰、可提取的答案，仍然可以被引用。

**重点关注：**
- Schema markup 是最大的杠杆——Article、FAQPage、HowTo 和 Product schemas 为 AI Overviews 提供结构化上下文（30-40% 可见性提升）
- 通过具有强内部链接的内容集群建立主题权威
- 在内容中包含命名的、有来源的引用（不仅仅是声明）
- 带有真实资质的作者简介很重要——E-E-A-T 权重很高
- 尽可能进入 Google 的 Knowledge Graph（准确的 Wikipedia 条目有帮助）
- 针对"如何做"和"什么是"查询模式——这些最常触发 AI Overviews

---

## ChatGPT

ChatGPT 的网络搜索基于 Bing 索引。它将其与训练知识结合生成答案，然后引用它所依赖的网络来源。

**ChatGPT 的不同之处：** 域名权威度在这里比其他 AI 平台更重要。SE Ranking 对 129,000 个域名的分析发现，权威度和可信度信号约占决定引用的 40%，内容质量约占 35%，平台信任占 25%。具有高引用域名计数（350K+）的网站平均每次响应获得 8.4 次引用，而信任分数略低的网站（91-96 vs 97-100）从 8.4 次下降到 6 次。

**新鲜度是一个主要区别。** 最近 30 天内更新的内容被引用的频率比旧内容高约 3.2 倍。ChatGPT 明显偏好最新信息。

**最重要的信号是内容-答案匹配**——ZipTie 对 400,000 个页面的分析发现，你的内容的风格和结构与 ChatGPT 自己的响应格式的匹配程度约占引用可能性的 55%。这远比域名权威度（12%）或页面结构（14%）单独重要。以 ChatGPT 回答问题的方式写作，你更有可能成为它引用的来源。

**ChatGPT 在你的网站之外查找的地方：** Wikipedia 占所有 ChatGPT 引用的 7.8%，Reddit 占 1.8%，Forbes 占 1.1%。品牌官方网站经常被引用，但第三方提及具有重要权重。

**重点关注：**
- 投资反向链接和域名权威度——这是最强的基础信号
- 至少每月更新竞争性内容
- 以 ChatGPT 构建答案的方式结构化你的内容（对话式、直接、组织良好）
- 包含带有命名来源的可验证统计数据
- 清晰的标题层次结构（H1 > H2 > H3）带有描述性标题

---

## Perplexity

Perplexity 始终附带可点击链接引用其来源，使其成为最透明的 AI 搜索平台。它将自己的索引与 Google 的索引结合，并通过多个重排序通道运行结果——初始相关性检索，然后传统排名因素评分，然后基于 ML 的质量评估，如果结果集未达到质量阈值，可以丢弃整个结果集。

**Perplexity 的不同之处：** 它是最"面向研究"的 AI 搜索引擎，其引用行为反映了这一点。Perplexity 维护权威域名的策划列表（Amazon、GitHub、主要学术网站），这些列表获得内在排名提升。它使用时间衰减算法快速评估新内容，为新发布者提供真正的引用机会。

**Perplexity 有独特的内容偏好：**
- **FAQ Schema (JSON-LD)** — 带有 FAQ 结构化数据的页面被引用的频率明显更高
- **PDF 文档** — 公开可访问的 PDF（白皮书、研究报告）被优先考虑。如果你有权威 PDF 内容被表单限制，考虑公开一个版本。
- **发布速度** — 你发布的频率比关键词定位更重要
- **自包含段落** — Perplexity 偏好可以干净提取的原子化、语义完整的段落

**重点关注：**
- 在 robots.txt 中允许 PerplexityBot
- 在任何带有问答内容的页面上实施 FAQPage schema
- 公开托管 PDF 资源（白皮书、指南、报告）
- 添加带有发布和修改时间戳的 Article schema
- 以清晰、自包含的段落写作，作为独立答案工作
- 在你的特定领域建立深度主题权威

---

## Microsoft Copilot

Copilot 嵌入在 Microsoft 的生态系统中——Edge、Windows、Microsoft 365 和 Bing Search。它完全依赖 Bing 的索引，所以如果 Bing 没有索引你的内容，Copilot 无法引用你。

**Copilot 的不同之处：** Microsoft 生态系统连接创造了独特的优化机会。LinkedIn 和 GitHub 上的提及和内容提供其他平台不提供的排名提升。Copilot 还更注重页面速度——低于 2 秒的加载时间是明确的阈值。

**重点关注：**
- 将你的网站提交到 Bing Webmaster Tools（许多网站只提交到 Google Search Console）
- 使用 IndexNow 协议更快地索引新内容和更新内容
- 将页面速度优化到 2 秒以下
- 编写清晰的实体定义——当你的内容定义术语或概念时，使定义明确且可提取
- 在 LinkedIn（发布文章、维护公司页面）和 GitHub（如果相关）上建立存在感
- 确保 Bingbot 具有完全爬取访问权限

---

## Claude

Claude 在启用网络搜索时使用 Brave Search 作为其搜索后端——不是 Google，不是 Bing。这是一个完全不同的索引，这意味着你的 Brave Search 可见性直接决定 Claude 是否能找到并引用你。

**Claude 的不同之处：** Claude 对其引用的内容非常挑剔。虽然它处理大量内容，但其引用率非常低——它在寻找给定主题上最准确、最有来源的内容。带有具体数字和清晰归属的数据丰富内容的表现明显优于通用内容。

**重点关注：**
- 验证你的内容是否出现在 Brave Search 结果中（在 search.brave.com 搜索你的品牌和关键术语）
- 在 robots.txt 中允许 ClaudeBot 和 anthropic-ai 用户代理
- 最大化事实密度——具体数字、命名来源、带日期的统计数据
- 使用清晰、可提取的结构和描述性标题
- 在内容中引用权威来源
- 力求成为你的主题上最准确的来源——Claude 奖励精确性

---

## 在 robots.txt 中允许 AI 机器人

如果你的 robots.txt 阻止了 AI 机器人，该平台无法引用你的内容。以下是需要允许的用户代理：

```
User-agent: GPTBot           # OpenAI — 支持 ChatGPT 搜索
User-agent: ChatGPT-User     # ChatGPT 浏览模式
User-agent: PerplexityBot    # Perplexity AI 搜索
User-agent: ClaudeBot        # Anthropic Claude
User-agent: anthropic-ai     # Anthropic Claude（备用）
User-agent: Google-Extended   # Google Gemini 和 AI Overviews
User-agent: Bingbot          # Microsoft Copilot（通过 Bing）
Allow: /
```

**训练 vs. 搜索：** 一些 AI 机器人同时用于模型训练和搜索引用。如果你想被引用但不希望你的内容用于训练，你的选择有限——GPTBot 为 OpenAI 处理两者。但是，你可以安全地阻止 **CCBot**（Common Crawl）而不影响任何 AI 搜索引用，因为它仅用于训练数据集收集。

---

## 从哪里开始

如果你是第一次为 AI 搜索进行优化，将精力集中在你的受众实际所在的地方：

**从 Google AI Overviews 开始** — 它们覆盖最多的用户（45%+ 的 Google 搜索），并且你可能已经拥有 Google SEO 基础。添加 schema markup，在内容中包含引用来源，并加强 E-E-A-T 信号。

**然后解决 ChatGPT** — 它是技术和商业受众中最常用的独立 AI 搜索工具。专注于新鲜度（每月更新内容）、域名权威度，并将你的内容结构与 ChatGPT 格式化其响应的方式匹配。

**然后扩展到 Perplexity** — 如果你的受众包括研究人员、早期采用者或技术专业人员，则特别有价值。添加 FAQ schema，发布 PDF 资源，并以清晰、自包含的段落写作。

**除非你的受众偏向企业/Microsoft（Copilot）或开发者/分析师（Claude），否则 Copilot 和 Claude 优先级较低。** 但基础知识——结构化内容、引用来源、schema markup——在所有平台上都有帮助。

**在任何地方都有帮助的行动：**
1. 在 robots.txt 中允许所有 AI 机器人
2. 实施 schema markup（至少 FAQPage、Article、Organization）
3. 在内容中包含带有命名来源的统计数据
4. 定期更新内容——竞争性主题每月一次
5. 使用清晰的标题结构（H1 > H2 > H3）
6. 将页面加载时间保持在 2 秒以下
7. 添加带有资质的作者简介
