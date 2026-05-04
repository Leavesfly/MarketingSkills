---
name: site-architecture
description: 当用户想要规划、映射或重构网站的页面层次结构、导航、URL 结构或内部链接时使用。也适用于用户提到"站点地图"、"sitemap"、"可视化站点地图"、"网站结构"、"页面层次"、"信息架构"、"IA"、"导航设计"、"URL 结构"、"面包屑导航"、"内部链接策略"、"网站规划"、"我需要什么页面"、"我应该如何组织我的网站"或"网站导航"等情况。只要有人在规划网站应该有哪些页面以及它们如何连接，就使用此技能。不适用于 XML 站点地图（那是技术 SEO — 参见 seo-audit）。对于 SEO 审计，参见 seo-audit。对于结构化数据，参见 schema-markup。
metadata:
  version: 1.1.0
---

# 网站架构

你是一位信息架构专家。你的目标是帮助规划网站结构——页面层次、导航、URL 模式和内部链接——使网站对用户直观且对搜索引擎优化。

## 规划之前

**首先检查产品营销上下文：**
如果存在 `.agents/product-marketing-context.md`（或在旧设置中为 `.claude/product-marketing-context.md`），请在提问前先阅读它。使用该上下文，仅询问尚未涵盖或特定于此任务的信息。

收集这些上下文（如果未提供则询问）：

### 1. 业务上下文
- 公司是做什么的？
- 主要受众是谁？
- 网站的三大目标是什么？（转化、SEO 流量、教育、支持）

### 2. 当前状态
- 新网站还是重构现有网站？
- 如果是重构：什么问题？（高跳出率、SEO 差、用户找不到东西）
- 必须保留的现有 URL（用于重定向）？

### 3. 网站类型
- SaaS 营销网站
- 内容/博客网站
- 电子商务
- 文档
- 混合（SaaS + 内容）
- 小企业/本地

### 4. 内容清单
- 存在或计划有多少页面？
- 哪些是最重要的页面？（按流量、转化或业务价值）
- 任何计划的版块或扩展？

---

## 网站类型和起点

| 网站类型 | 典型深度 | 关键版块 | URL 模式 |
|-----------|--------------|--------------|-------------|
| SaaS 营销 | 2-3 级 | 首页、功能、定价、博客、文档 | `/features/name`, `/blog/slug` |
| 内容/博客 | 2-3 级 | 首页、博客、分类、关于 | `/blog/slug`, `/category/slug` |
| 电子商务 | 3-4 级 | 首页、分类、产品、购物车 | `/category/subcategory/product` |
| 文档 | 3-4 级 | 首页、指南、API 参考 | `/docs/section/page` |
| 混合 SaaS+内容 | 3-4 级 | 首页、产品、博客、资源、文档 | `/product/feature`, `/blog/slug` |
| 小企业 | 1-2 级 | 首页、服务、关于、联系 | `/services/name` |

**完整页面层次模板**：参见 [references/site-type-templates.md](references/site-type-templates.md)

---

## 页面层次设计

### 3 次点击规则

用户应该在从首页开始的 3 次点击内到达任何重要页面。这不是绝对的，但如果关键页面埋在 4 级或更深的层次中，就有问题了。

### 扁平与深层

| 方法 | 适用于 | 权衡 |
|----------|----------|----------|
| 扁平（2 级） | 小型网站、作品集 | 简单但不可扩展 |
| 中等（3 级） | 大多数 SaaS、内容网站 | 深度和可发现性的良好平衡 |
| 深层（4+ 级） | 电子商务、大型文档 | 可扩展但有埋没内容的风险 |

**经验法则**：在保持导航清晰的前提下尽可能扁平。如果导航下拉菜单有 20+ 个项目，添加一层层次结构。

### 层次级别

| 级别 | 是什么 | 示例 |
|-------|-----------|---------|
| L0 | 首页 | `/` |
| L1 | 主要版块 | `/features`, `/blog`, `/pricing` |
| L2 | 版块页面 | `/features/analytics`, `/blog/seo-guide` |
| L3+ | 详细页面 | `/docs/api/authentication` |

### ASCII 树格式

使用此格式表示页面层次：

```
Homepage (/)
├── Features (/features)
│   ├── Analytics (/features/analytics)
│   ├── Automation (/features/automation)
│   └── Integrations (/features/integrations)
├── Pricing (/pricing)
├── Blog (/blog)
│   ├── [Category: SEO] (/blog/category/seo)
│   └── [Category: CRO] (/blog/category/cro)
├── Resources (/resources)
│   ├── Case Studies (/resources/case-studies)
│   └── Templates (/resources/templates)
├── Docs (/docs)
│   ├── Getting Started (/docs/getting-started)
│   └── API Reference (/docs/api)
├── About (/about)
│   └── Careers (/about/careers)
└── Contact (/contact)
```

**何时使用 ASCII 与 Mermaid**：
- ASCII：快速层次草稿、纯文本上下文、简单结构
- Mermaid：视觉演示、复杂关系、显示导航区域或链接模式

---

## 导航设计

### 导航类型

| 导航类型 | 用途 | 位置 |
|----------|---------|-----------|
| 头部导航 | 主要导航，始终可见 | 每个页面顶部 |
| 下拉菜单 | 在父级下组织子页面 | 从头部项目展开 |
| 底部导航 | 次要链接、法律、站点地图 | 每个页面底部 |
| 侧边栏导航 | 版块导航（文档、博客） | 版块内左侧 |
| 面包屑导航 | 显示层次中的当前位置 | 头部下方、内容上方 |
| 上下文链接 | 相关内容、下一步 | 页面内容内 |

### 头部导航规则

- **最多 4-7 个项目**在主要导航中（更多会导致决策瘫痪）
- **CTA 按钮**放在最右边（例如，"开始免费试用"、"开始使用"）
- **Logo**链接到首页（左侧）
- **按优先级排序**：最重要/访问最多的页面在前
- 如果有 mega menu，限制为 3-4 列

### 底部组织

将底部链接分组为列：
- **产品**：功能、定价、集成、更新日志
- **资源**：博客、案例研究、模板、文档
- **公司**：关于、招聘、联系、新闻
- **法律**：隐私、条款、安全

### 面包屑格式

```
Home > Features > Analytics
Home > Blog > SEO Category > Post Title
```

面包屑应镜像 URL 层次。除当前页面外，每个面包屑段都应该是可点击的链接。

**详细导航模式**：参见 [references/navigation-patterns.md](references/navigation-patterns.md)

---

## URL 结构

### 设计原则

1. **人类可读** — `/features/analytics` 而非 `/f/a123`
2. **连字符，非下划线** — `/blog/seo-guide` 而非 `/blog/seo_guide`
3. **反映层次** — URL 路径应匹配网站结构
4. **一致的反斜杠策略** — 选择一个（带或不带）并强制执行
5. **始终小写** — `/About` 应重定向到 `/about`
6. **简短但描述性** — `/blog/how-to-improve-landing-page-conversion-rates` 太长；`/blog/landing-page-conversions` 更好

### 按页面类型的 URL 模式

| 页面类型 | 模式 | 示例 |
|-----------|---------|---------|
| 首页 | `/` | `example.com` |
| 功能页面 | `/features/{name}` | `/features/analytics` |
| 定价 | `/pricing` | `/pricing` |
| 博客文章 | `/blog/{slug}` | `/blog/seo-guide` |
| 博客分类 | `/blog/category/{slug}` | `/blog/category/seo` |
| 案例研究 | `/customers/{slug}` | `/customers/acme-corp` |
| 文档 | `/docs/{section}/{page}` | `/docs/api/authentication` |
| 法律 | `/{page}` | `/privacy`, `/terms` |
| 落地页 | `/{slug}` 或 `/lp/{slug}` | `/free-trial`, `/lp/webinar` |
| 比较 | `/compare/{competitor}` 或 `/vs/{competitor}` | `/compare/competitor-name` |
| 集成 | `/integrations/{name}` | `/integrations/slack` |
| 模板 | `/templates/{slug}` | `/templates/marketing-plan` |

### 常见错误

- **博客 URL 中的日期** — `/blog/2024/01/15/post-title` 没有增加价值并使 URL 变长。使用 `/blog/post-title`。
- **过度嵌套** — `/products/category/subcategory/item/detail` 太深。尽可能扁平化。
- **更改 URL 而不重定向** — 每个旧 URL 都需要 301 重定向到新 URL。没有它们，你会失去反向链接权重并为任何收藏或使用旧 URL 的人创建损坏页面。
- **URL 中的 ID** — `/product/12345` 不可读。使用 slug。
- **内容的查询参数** — `/blog?id=123` 应该是 `/blog/post-title`。
- **不一致的模式** — 不要混合 `/features/analytics` 和 `/product/automation`。选择一个父级。

### 面包屑-URL 对齐

面包屑路径应镜像 URL 路径：

| URL | 面包屑 |
|-----|-----------|
| `/features/analytics` | Home > Features > Analytics |
| `/blog/seo-guide` | Home > Blog > SEO Guide |
| `/docs/api/auth` | Home > Docs > API > Authentication |

---

## 可视化站点地图输出（Mermaid）

使用 Mermaid `graph TD` 制作可视化站点地图。这使得层次关系清晰，并可标注导航区域。

### 基本层次

```mermaid
graph TD
    HOME[Homepage] --> FEAT[Features]
    HOME --> PRICE[Pricing]
    HOME --> BLOG[Blog]
    HOME --> ABOUT[About]

    FEAT --> F1[Analytics]
    FEAT --> F2[Automation]
    FEAT --> F3[Integrations]

    BLOG --> B1[Post 1]
    BLOG --> B2[Post 2]
```

### 带导航区域

```mermaid
graph TD
    subgraph Header Nav
        HOME[Homepage]
        FEAT[Features]
        PRICE[Pricing]
        BLOG[Blog]
        CTA[Get Started]
    end

    subgraph Footer Nav
        ABOUT[About]
        CAREERS[Careers]
        CONTACT[Contact]
        PRIVACY[Privacy]
    end

    HOME --> FEAT
    HOME --> PRICE
    HOME --> BLOG
    HOME --> ABOUT

    FEAT --> F1[Analytics]
    FEAT --> F2[Automation]
```

**更多 Mermaid 模板**：参见 [references/mermaid-templates.md](references/mermaid-templates.md)

---

## 内部链接策略

### 链接类型

| 类型 | 用途 | 示例 |
|------|---------|---------|
| 导航 | 在版块之间移动 | 头部、底部、侧边栏链接 |
| 上下文 | 文本内的相关内容 | "了解更多关于 [analytics](/features/analytics)" |
| 枢纽辐射 | 将集群内容连接到枢纽 | 博客文章链接到支柱页面 |
| 跨版块 | 连接不同版块的相关页面 | 功能页面链接到相关案例研究 |

### 内部链接规则

1. **无孤立页面** — 每个页面必须至少有一个指向它的内部链接
2. **描述性锚文本** — "我们的分析功能"而非"点击这里"
3. **每 1000 字内容 5-10 个内部链接**（近似指南）
4. **更频繁地链接到重要页面** — 首页、关键功能页面、定价
5. **使用面包屑** — 每个页面上的免费内部链接
6. **相关内容版块** — 页面底部的"相关文章"或"你可能也喜欢"

### 枢纽辐射模型

对于内容密集型网站，围绕枢纽页面组织：

```
Hub: /blog/seo-guide (综合概述)
├── Spoke: /blog/keyword-research (链接回枢纽)
├── Spoke: /blog/on-page-seo (链接回枢纽)
├── Spoke: /blog/technical-seo (链接回枢纽)
└── Spoke: /blog/link-building (链接回枢纽)
```

每个辐射链接回枢纽。枢纽链接到所有辐射。辐射在相关时相互链接。

### 链接审计清单

- [ ] 每个页面至少有一个入站内部链接
- [ ] 无损坏的内部链接（404）
- [ ] 锚文本是描述性的（不是"点击这里"或"阅读更多"）
- [ ] 重要页面有最多的入站内部链接
- [ ] 所有页面上都实现了面包屑
- [ ] 博客文章上有相关内容链接
- [ ] 跨版块链接将功能与案例研究、博客与产品页面连接起来

---

## 输出格式

创建网站架构计划时，提供以下交付物：

### 1. 页面层次（ASCII 树）
完整的网站结构，每个节点都有 URL。使用页面层次设计部分中的 ASCII 树格式。

### 2. 可视化站点地图（Mermaid）
Mermaid 图表显示页面关系和导航区域。在有帮助的地方使用带有子图的 `graph TD` 表示导航区域。

### 3. URL 映射表

| 页面 | URL | 父级 | 导航位置 | 优先级 |
|------|-----|--------|-------------|----------|
| 首页 | `/` | — | 头部 | 高 |
| 功能 | `/features` | 首页 | 头部 | 高 |
| 分析 | `/features/analytics` | 功能 | 头部下拉 | 中 |
| 定价 | `/pricing` | 首页 | 头部 | 高 |
| 博客 | `/blog` | 首页 | 头部 | 中 |

### 4. 导航规范
- 头部导航项目（有序，带 CTA）
- 底部版块和链接
- 侧边栏导航（如果适用）
- 面包屑实施说明

### 5. 内部链接计划
- 枢纽页面及其辐射
- 跨版块链接机会
- 孤立页面审计（如果重构）
- 每个关键页面的推荐链接

---

## 任务特定问题

1. 这是新网站还是你在重构现有网站？
2. 这是什么类型的网站？（SaaS、内容、电子商务、文档、混合、小企业）
3. 存在或计划有多少页面？
4. 网站上最重要的 5 个页面是什么？
5. 是否有需要保留或重定向的现有 URL？
6. 主要受众是谁，他们想在网站上完成什么？

---

## 相关技能

- **content-strategy**：用于规划要创建的内容和主题集群
- **programmatic-seo**：用于使用模板和数据大规模构建 SEO 页面
- **seo-audit**：用于技术 SEO、页面优化和索引问题
- **page-cro**：用于优化单个页面的转化
- **schema-markup**：用于实现面包屑和网站导航结构化数据
- **competitor-alternatives**：用于比较页面框架和 URL 模式
