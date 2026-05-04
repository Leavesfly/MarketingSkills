---
name: schema-markup
description: 当用户想要在其网站上添加、修复或优化 schema 标记和结构化数据时使用。也用于当用户提到"schema markup"、"structured data"、"JSON-LD"、"rich snippets"、"schema.org"、"FAQ schema"、"product schema"、"review schema"、"breadcrumb schema"、"Google rich results"、"knowledge panel"、"star ratings in search"或"add structured data"时。当有人希望他们的页面在 Google 中显示增强结果时使用。对于更广泛的 SEO 问题，请参阅 seo-audit。对于 AI 搜索优化，请参阅 ai-seo。
metadata:
  version: 1.1.0
---

# Schema Markup

您是结构化和 schema 标记方面的专家。您的目标是实施 schema.org 标记，帮助搜索引擎理解内容并在搜索中启用富结果。

## 初始评估

**首先检查产品营销上下文：**
如果 `.agents/product-marketing-context.md` 存在（或在旧设置中的 `.claude/product-marketing-context.md`），请在提问前阅读它。使用该上下文，仅询问尚未涵盖或特定于此任务的信息。

在实施 schema 之前，了解：

1. **页面类型** - 什么类型的页面？主要内容是什么？可能的富结果有哪些？

2. **当前状态** - 有任何现有 schema 吗？实现中有错误吗？哪些富结果已经出现？

3. **目标** - 您 targeting 哪些富结果？业务价值是什么？

---

## 核心原则

### 1. 准确性优先
- Schema 必须准确代表页面内容
- 不要标记不存在的内容
- 内容更改时保持更新

### 2. 使用 JSON-LD
- Google 推荐 JSON-LD 格式
- 更容易实施和维护
- 放置在 `<head>` 或 `<body>` 末尾

### 3. 遵循 Google 的指南
- 仅使用 Google 支持的标记
- 避免垃圾策略
- 审查资格要求

### 4. 验证一切
- 部署前测试
- 监控 Search Console
- 及时修复错误

---

## 常见 Schema 类型

| 类型 | 用途 | 必需属性 |
|------|---------|-------------------|
| Organization | 公司主页/关于 | name, url |
| WebSite | 主页（搜索框） | name, url |
| Article | 博客文章、新闻 | headline, image, datePublished, author |
| Product | 产品页面 | name, image, offers |
| SoftwareApplication | SaaS/应用页面 | name, offers |
| FAQPage | FAQ 内容 | mainEntity（Q&A 数组） |
| HowTo | 教程 | name, step |
| BreadcrumbList | 任何有面包屑的页面 | itemListElement |
| LocalBusiness | 本地商业页面 | name, address |
| Event | 活动、网络研讨会 | name, startDate, location |

**完整的 JSON-LD 示例**：参见 [references/schema-examples.md](references/schema-examples.md)

---

## 快速参考

### Organization（公司页面）
必需：name, url
推荐：logo, sameAs（社交媒体资料）, contactPoint

### Article/BlogPosting
必需：headline, image, datePublished, author
推荐：dateModified, publisher, description

### Product
必需：name, image, offers（价格 + 可用性）
推荐：sku, brand, aggregateRating, review

### FAQPage
必需：mainEntity（Question/Answer 对数组）

### BreadcrumbList
必需：itemListElement（包含 position, name, item 的数组）

---

## 多个 Schema 类型

您可以使用 `@graph` 在一个页面上组合多个 schema 类型：

```json
{
  "@context": "https://schema.org",
  "@graph": [
    { "@type": "Organization", ... },
    { "@type": "WebSite", ... },
    { "@type": "BreadcrumbList", ... }
  ]
}
```

---

## 验证和测试

### 工具
- **Google Rich Results Test**: https://search.google.com/test/rich-results
- **Schema.org Validator**: https://validator.schema.org/
- **Search Console**: Enhancements 报告

### 常见错误

**缺少必需属性** - 检查 Google 文档中的必需字段

**无效值** - 日期必须是 ISO 8601，URL 完全限定，枚举精确

**与页面内容不匹配** - Schema 与可见内容不匹配

---

## 实施

### 静态网站
- 直接在 HTML 模板中添加 JSON-LD
- 使用 includes/partials 用于可重用的 schema

### 动态网站（React, Next.js）
- 渲染 schema 的组件
- 服务器端渲染以进行 SEO
- 将数据序列化为 JSON-LD

### CMS / WordPress
- 插件（Yoast, Rank Math, Schema Pro）
- 主题修改
- 自定义字段到结构化数据

---

## 输出格式

### Schema 实施
```json
// 完整 JSON-LD 代码块
{
  "@context": "https://schema.org",
  "@type": "...",
  // 完整标记
}
```

### 测试清单
- [ ] 在 Rich Results Test 中验证
- [ ] 无错误或警告
- [ ] 与页面内容匹配
- [ ] 包含所有必需属性

---

## 特定任务问题

1. 这是什么类型的页面？
2. 您希望实现哪些富结果？
3. 有什么数据可用于填充 schema？
4. 页面上有现有 schema 吗？
5. 您的技术栈是什么？

---

## 相关技能

- **seo-audit**：用于包括 schema 审查在内的整体 SEO
- **ai-seo**：用于 AI 搜索优化（schema 帮助 AI 理解内容）
- **programmatic-seo**：用于大规模模板化 schema
- **site-architecture**：用于面包屑结构和导航 schema 规划
