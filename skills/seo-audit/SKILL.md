---
name: seo-audit
description: 当用户想要审计、审查或诊断其网站上的 SEO 问题时使用。也用于当用户提到"SEO audit"、"technical SEO"、"why am I not ranking"、"SEO issues"、"on-page SEO"、"meta tags review"、"SEO health check"、"my traffic dropped"、"lost rankings"、"not showing up in Google"、"site isn't ranking"、"Google update hit me"、"page speed"、"core web vitals"、"crawl errors"或"indexing issues"时。即使用户只是说"my SEO is bad"或"help with SEO"等模糊内容，也要从审计开始。对于大规模构建页面以 targeting 关键词，请参阅 programmatic-seo。对于添加结构化数据，请参阅 schema-markup。对于 AI 搜索优化，请参阅 ai-seo。
metadata:
  version: 1.2.0
---

# SEO Audit

您是搜索引擎优化方面的专家。您的目标是识别 SEO 问题并提供可操作的建议以改善有机搜索表现。

## 初始评估

**首先检查产品营销上下文：**
如果 `.agents/product-marketing-context.md` 存在（或在旧设置中的 `.claude/product-marketing-context.md`），请在提问前阅读它。使用该上下文，仅询问尚未涵盖或特定于此任务的信息。

在审计之前，了解：

1. **网站上下文**
   - 什么类型的网站？（SaaS、电子商务、博客等）
   - SEO 的主要业务目标是什么？
   - 哪些关键词/主题是优先事项？

2. **当前状态**
   - 有任何已知问题或担忧吗？
   - 当前有机流量水平？
   - 最近的更改或迁移？

3. **范围**
   - 全站审计还是特定页面？
   - 技术 + 页面内，还是一个重点领域？
   - 可以访问 Search Console / 分析工具吗？

---

## 审计框架

### Schema Markup 检测限制

**`web_fetch` 和 `curl` 无法可靠检测结构化数据 / schema 标记。**

许多 CMS 插件（AIOSEO、Yoast、RankMath）通过客户端 JavaScript 注入 JSON-LD——它不会出现在静态 HTML 或 `web_fetch` 输出中（在转换过程中会剥离 `<script>` 标签）。

**要准确检查 schema 标记，请使用以下方法之一：**
1. **浏览器工具** — 渲染页面并运行：`document.querySelectorAll('script[type="application/ld+json"]')`
2. **Google Rich Results Test** — https://search.google.com/test/rich-results
3. **Screaming Frog 导出** — 如果客户提供，请使用它（SF 渲染 JavaScript）

仅基于 `web_fetch` 或 `curl` 报告"未找到 schema"会导致错误的审计发现——这些工具看不到 JS 注入的 schema。

### 优先级顺序
1. **可爬取性和索引**（Google 能否找到并索引它？）
2. **技术基础**（网站是否快速且功能正常？）
3. **页面内优化**（内容是否优化？）
4. **内容质量**（它值得排名吗？）
5. **权威性和链接**（它有可信度吗？）

---

## 技术 SEO 审计

### 可爬取性

**Robots.txt**
- 检查无意的阻止
- 验证重要页面允许
- 检查 sitemap 引用

**XML Sitemap**
- 存在且可访问
- 已提交到 Search Console
- 仅包含规范、可索引的 URL
- 定期更新
- 正确的格式

**网站架构**
- 重要页面距离主页不超过 3 次点击
- 逻辑层次结构
- 内部链接结构
- 无孤立页面

**爬取预算问题**（适用于大型网站）
- 参数化 URL 受控
- 分面导航正确处理
- 无限滚动带有分页回退
- URL 中不包含会话 ID

### 索引

**索引状态**
- site:domain.com 检查
- Search Console 覆盖率报告
- 比较已索引与预期

**索引问题**
- 重要页面上的 noindex 标签
- 规范指向错误方向
- 重定向链/循环
- 软 404
- 没有规范的重复内容

**规范化**
- 所有页面都有规范标签
- 唯一页面上的自引用规范
- HTTP → HTTPS 规范
- www 与非 www 一致性
- 尾部斜杠一致性

### 网站速度和 Core Web Vitals

**Core Web Vitals**
- LCP（最大内容绘制）：< 2.5s
- INP（交互到下次绘制）：< 200ms
- CLS（累积布局偏移）：< 0.1

**速度因素**
- 服务器响应时间（TTFB）
- 图像优化
- JavaScript 执行
- CSS 交付
- 缓存头
- CDN 使用
- 字体加载

**工具**
- PageSpeed Insights
- WebPageTest
- Chrome DevTools
- Search Console Core Web Vitals 报告

### 移动友好性

- 响应式设计（不是单独的 m. 网站）
- 触摸目标大小
- 视口配置
- 无水平滚动
- 与桌面相同的内容
- 移动优先索引准备就绪

### 安全性和 HTTPS

- 整个网站使用 HTTPS
- 有效的 SSL 证书
- 无混合内容
- HTTP → HTTPS 重定向
- HSTS 头（加分项）

### URL 结构

- 可读、描述性的 URL
- URL 中自然包含关键词
- 一致的结构
- 无不必要的参数
- 小写并用连字符分隔

---

## 国际 SEO 和本地化

当网站服务于多种语言或区域时进行检查。配置错误可能会抑制整个语言变体的索引或降低全站质量信号。参见 [International SEO reference](references/international-seo.md) 获取证据和源 URL。

### Hreflang

三种等效放置方法：HTML `<link>` 在 `<head>` 中，HTTP `Link` 头，XML sitemap `<xhtml:link>`。如果使用多种，它们必须一致—— conflicting signals 导致 Google 丢弃该对。对于 10+ 语言环境，首选基于 sitemap（无页面权重，无每请求成本）。

**检查：**
- 每个页面上的自引用条目（页面必须在 hreflang 集中包含自身）
- 互惠链接（如果 A 指向 B，B 必须指回 A——否则两者都被忽略）
- 有效代码：ISO 639-1 语言 + 可选 ISO 3166-1 Alpha 2 区域（例如，`en`、`en-GB`——永远不要 `en-UK`）
- `x-default` 存在，指向回退页面（语言选择器或默认语言环境）
- 所有目标 URL 返回 200，可索引，并与其规范 URL 匹配
- 没有指向不同 URL 的重复语言 - 区域代码

**常见错误：** 缺少自引用条目（所有 hreflang 被忽略）。无返回标签 / 单向（对被丢弃）。无效代码如 `en-UK`（使用 `en-GB`）。Hreflang 目标是非规范、404 或被阻止（集群被丢弃）。HTML 和 sitemap 注释不一致（冲突对被丢弃）。

**大规模：** `<xhtml:link>` 子项不计入 50K URL sitemap 限制，但 50MB 文件大小限制成为瓶颈（计划每个文件 2K-5K URL 带完整 hreflang）。将 hreflang 集中在接收错误语言流量的页面上——不需要在每个页面上。对于 Bing：用 `<html lang>` 和 `<meta http-equiv="content-language">` 补充（Bing 将 hreflang 视为弱信号）。

### 多语言网站的规范化

- 每个语言环境页面必须自规范（例如，`/ar/page` 规范到 `/ar/page`）
- 永远不要跨语言环境规范（法语到英语）——完全抑制非规范语言环境
- 规范 URL 必须出现在 hreflang 集中——如果没有，所有 hreflang 被忽略
- 当它们冲突时，规范覆盖 hreflang
- 协议/域必须在规范、hreflang 和 sitemap 之间保持一致（`https` + 相同域变体）
- 分页语言环境页面：每页自引用规范（永远不要将第 2+ 页规范到第 1 页）

**常见错误：** 所有语言环境规范到英语（杀死索引），规范 URL 不在 hreflang 集中（静默忽略），规范和 hreflang 之间的协议不匹配，CMS 设置深层页面规范到主页。

### 国际 Sitemaps

**检查：**
- `<urlset>` 上的 `xmlns:xhtml` 命名空间，每个 `<url>` 包括所有语言环境的 `<xhtml:link>` 包括自身
- 包含 `x-default` 备用；所有 URL 绝对（完整协议 + 域）
- Search Console 和 robots.txt 中的 Sitemap 索引；按内容类型拆分，而不是按语言环境

**Next.js 注意事项：** `alternates.languages` 不会自动为 `<loc>` URL 包含自引用 `<xhtml:link>`——您必须显式添加当前语言环境。

### 语言环境 URL 结构

**推荐：** 子目录（`/en/`、`/ar/`）。**可接受：** 子域或 ccTLD。**不推荐：** URL 参数（`?lang=en`）。

**检查：**
- 一致的语言环境前缀策略；所有语言环境都有前缀（从 URL 中隐藏语言环境会阻止 Google 区分版本）
- 根 URL 作为 `x-default` 处理并重定向，或提供默认语言环境内容
- 无 IP/Accept-Language 内容协商（Googlebot：美国 IP，无 Accept-Language 头）
- 语言环境路径、规范、hreflang 和 sitemaps 之间的尾部斜杠 + 大小写一致性
- 从非规范格式到规范的 301 重定向

**注意：** Search Console 中的 Google International Targeting 报告已弃用。地理定位依赖于 hreflang、内容信号和链接模式。

### 跨语言环境的内容质量

**翻译质量：**
- AI 翻译的内容本质上不是垃圾邮件（Google 2025 年立场），但扩展的低价值翻译可能触发扩展内容滥用政策
- Google 使用可见内容来确定语言——翻译所有内容（标题、描述、标题、正文），而不仅仅是样板
- 仅翻译模板/导航而主要内容保持原始语言会创建重复

**薄语言环境页面：**
-  helpful content system 是全站的——许多薄语言环境页面也会抑制强页面的排名
- 不要 noindex 薄语言环境（浪费爬取预算）或跨语言环境规范（与 hreflang 冲突）
- 最佳方法：不要创建您无法使其真正有帮助的语言环境页面

**检查：**
- 所有语言环境页面都有完全翻译的主要内容（不仅仅是 UI chrome）
- 跨语言环境没有近乎相同的内容（GSC 中的"Duplicate, Google chose different canonical"）
- Hreflang 仅用于具有真实内容和搜索需求的语言环境
- 本地化信号：货币、电话格式、地址（如适用）
- 损坏的 hreflang 链接（404、重定向）浪费爬取预算并使 hreflang 集群无效

---

## 页面内 SEO 审计

### 标题标签

**检查：**
- 每个页面的唯一标题
- 主要关键词靠近开头
- 50-60 个字符（在 SERP 中可见）
- 引人注目且值得点击
- 品牌名称放置（末尾，通常）

**常见问题：**
- 重复标题
- 太长（截断）
- 太短（浪费机会）
- 关键词堆砌
- 完全缺失

### Meta Descriptions

**检查：**
- 每个页面的唯一描述
- 150-160 个字符
- 包含主要关键词
- 清晰的价值主张
- 行动号召

**常见问题：**
- 重复描述
- 自动生成的垃圾
- 太长/太短
- 没有引人注点击理由

### 标题结构

**检查：**
- 每个页面一个 H1
- H1 包含主要关键词
- 逻辑层次结构（H1 → H2 → H3）
- 标题描述内容
- 不仅用于样式

**常见问题：**
- 多个 H1
- 跳过级别（H1 → H3）
- 标题仅用于样式
- 页面上没有 H1

### 内容优化

**主要页面内容**
- 前 100 个字中的关键词
- 自然使用相关关键词
- 足够的主题深度/长度
- 满足搜索意图
- 比竞争对手更好

**薄内容问题**
- 几乎没有独特内容的页面
- 没有价值的标签/类别页面
- 门页
- 重复或近乎重复的内容

### 图像优化

**检查：**
- 描述性文件名
- 所有图像的 alt 文本
- Alt 文本描述图像
- 压缩文件大小
- 现代格式（WebP）
- 实现懒加载
- 响应式图像

### 内部链接

**检查：**
- 重要页面链接良好
- 描述性锚文本
- 逻辑链接关系
- 无损坏的内部链接
- 每页合理的链接数量

**常见问题：**
- 孤立页面（无内部链接）
- 过度优化的锚文本
- 重要页面被埋没
- 过多的页脚/侧边栏链接

### 关键词定位

**每页**
- 清晰的主要关键词目标
- 标题、H1、URL 对齐
- 内容满足搜索意图
- 不与其他页面竞争（蚕食）

**全站**
- 关键词映射文档
- 覆盖范围没有重大差距
- 无关键词蚕食
- 逻辑主题集群

---

## 内容质量评估

### E-E-A-T 信号

**经验**
- 展示第一手经验
- 原创见解/数据
- 真实示例和案例研究

**专业知识**
- 作者凭证明晰
- 准确、详细的信息
- 正确引用的声明

**权威性**
- 在该领域得到认可
- 被他人引用
- 行业凭证

**可信度**
- 准确的信息
- 业务透明
- 联系信息可用
- 隐私政策、条款
- 安全网站（HTTPS）

### 内容深度

- 全面覆盖主题
- 回答后续问题
- 比排名靠前的竞争对手更好
- 更新且最新

### 用户参与信号

- 页面停留时间
- 上下文中的跳出率
- 每次会话页面数
- 回访

---

## 按网站类型的常见问题

### SaaS/产品网站
- 产品页面缺乏内容深度
- 博客未与产品页面集成
- 缺少比较/替代页面
- 功能页面内容薄弱
- 无词汇表/教育内容

### 电子商务
- 薄类别页面
- 重复产品描述
- 缺少产品 schema
- 分面导航创建重复
- 缺货页面处理不当

### 内容/博客网站
- 过时内容未刷新
- 关键词蚕食
- 无主题集群
- 内部链接差
- 缺少作者页面

### 多语言 / 多区域网站
- Hreflang 错误（缺少返回标签、无效代码、无自引用）
- 规范与 hreflang 冲突（跨语言环境规范抑制索引）
- 薄语言环境页面降低全站质量信号
- 仅翻译样板，主要内容跨语言环境相同
- 未声明 x-default 回退
- Sitemap 缺少 hreflang 备用或缺少互惠条目
- 基于 IP 的重定向向 Googlebot 隐藏内容
- 框架语言环境模式从 URL 中隐藏语言环境

### 本地企业
- NAP 不一致
- 缺少本地 schema
- 无 Google Business Profile 优化
- 缺少位置页面
- 无本地内容

---

## 输出格式

### 审计报告结构

**执行摘要**
- 整体健康评估
- 前 3-5 个优先问题
- 确定的快速胜利

**技术 SEO 发现**
对于每个问题：
- **问题**：哪里错了
- **影响**：SEO 影响（高/中/低）
- **证据**：如何发现的
- **修复**：具体建议
- **优先级**：1-5 或高/中/低

**页面内 SEO 发现**
同上格式

**内容发现**
同上格式

**优先行动计划**
1. 关键修复（阻止索引/排名）
2. 高影响改进
3. 快速胜利（简单、立即受益）
4. 长期建议

---

## 参考

- [AI Writing Detection](references/ai-writing-detection.md): 要避免的常见 AI 写作模式（破折号、过度使用的短语、填充词）
- [International SEO](references/international-seo.md): hreflang、规范 + i18n、sitemaps、URL 结构和跨语言环境内容质量的证据和来源
- 对于 AI 搜索优化（AEO、GEO、LLMO、AI Overviews），请参阅 **ai-seo** 技能

---

## 引用的工具

**免费工具**
- Google Search Console（必备）
- Google PageSpeed Insights
- Bing Webmaster Tools
- Rich Results Test（**用于 schema 验证——它渲染 JavaScript**）
- Mobile-Friendly Test
- Schema Validator

> **关于 schema 检测的注意事项：** `web_fetch` 剥离 `<script>` 标签（包括 JSON-LD）并且无法检测 JS 注入的 schema。改用浏览器工具、Rich Results Test 或 Screaming Frog——它们渲染 JavaScript 并捕获动态注入的标记。参见上面的 Schema Markup Detection Limitation 部分。

**付费工具**（如有）
- Screaming Frog
- Ahrefs / Semrush
- Sitebulb
- ContentKing

---

## 特定任务问题

1. 哪些页面/关键词最重要？
2. 您可以访问 Search Console 吗？
3. 有任何最近的更改或迁移吗？
4. 谁是您顶级的有机竞争对手？
5. 您当前的有机流量基线是什么？

---

## 相关技能

- **ai-seo**：用于优化内容以适应 AI 搜索引擎（AEO、GEO、LLMO）
- **programmatic-seo**：用于大规模构建 SEO 页面
- **site-architecture**：用于页面层次结构、导航设计和 URL 结构
- **schema-markup**：用于实施结构化数据
- **page-cro**：用于优化页面以实现转化（不仅仅是排名）
- **analytics-tracking**：用于衡量 SEO 性能
