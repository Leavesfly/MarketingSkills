# 国际 SEO：证据与来源

支持 SEO 审核技能中国际 SEO 和本地化部分的详细证据。按主题组织，包含来源 URL 和关键引用。

---

## Hreflang

### 放置方法

Google 支持三种等效方法：`<head>` 中的 HTML `<link>`、HTTP `Link` 标头以及 XML sitemap 中的 `<xhtml:link>` 元素。Google 确认没有任何方法优先于其他方法。

Google 会合并来自 HTML 和 sitemap 的信号。如果相同的语言-地区对在不同方法中指向不同的 URL，Google 会丢弃该配对而不是猜测。

- [Google Search Central：本地化版本](https://developers.google.com/search/docs/specialty/international/localized-versions)
- [SEJ：Google 合并 Hreflang 信号](https://www.searchenginejournal.com/google-combines-hreflang-signals-from-html-sitemaps/389219/)

### 互惠要求

Google 文档指出："如果页面 X 链接到页面 Y，页面 Y 必须链接回页面 X。否则，这些注释可能会被忽略或无法正确解释。"

每个页面都必须在 hreflang 集合中包含自身（自引用）。Semrush 审核发现，缺少自引用是第 1 大错误。一项针对 374,756 个域名的研究发现，67% 的 hreflang 实现存在问题。

- [Google Search Central：本地化版本](https://developers.google.com/search/docs/specialty/international/localized-versions)
- [Semrush：9 个常见的 Hreflang 错误](https://www.semrush.com/blog/hreflang-errors/)
- [SE Land：31% 的国际网站包含 Hreflang 错误](https://searchengineland.com/study-31-of-international-websites-contain-hreflang-errors-395161)

### x-default

于 2013 年 4 月推出。为语言/地区与任何声明的变体都不匹配的用户指定回退页面。可以指向与某个语言特定变体相同的 URL。必须在每个变体页面的完整注释集中包含。

- [Google Blog：x-default hreflang](https://developers.google.com/search/blog/2013/04/x-default-hreflang-for-international-pages)
- [Google Blog：x-default 如何帮助您（2023）](https://developers.google.com/search/blog/2023/05/x-default)

### 语言和地区代码

语言：ISO 639-1（2 字母）。地区：ISO 3166-1 Alpha 2（2 字母）。格式：`language[-script][-region]`。

您不能单独指定地区代码。常见错误：`en-UK`（应为 `en-GB`）、`es-419`（非 ISO 3166-1）。一项研究发现，8.9% 使用 hreflang 的网站包含无效的语言代码。

- [Google Search Central：本地化版本](https://developers.google.com/search/docs/specialty/international/localized-versions)
- [SE Land：31% 研究](https://searchengineland.com/study-31-of-international-websites-contain-hreflang-errors-395161)

### 大规模 Hreflang（20+ 语言环境）

对于 20 种语言环境，HTML `<head>` 中的 hreflang 会为每个页面增加约 1.5KB，而对用户毫无益处。基于 sitemap 的 hreflang 对运行时性能零影响。`<xhtml:link>` 子元素不计入 50,000 URL 的 sitemap 限制（只有 `<loc>` 元素计入）。

John Mueller 建议将 hreflang 集中在收到错误语言流量的页面上，而不是每个页面："我不会为网站的其他任何页面这样做，因为它太复杂且难以管理。"

- [SERoundtable：子元素不计入限制](https://www.seroundtable.com/google-child-elements-dont-count-towards-sitemap-url-limit-34377.html)
- [SERoundtable：Hreflang 应聚焦何处](https://www.seroundtable.com/using-hreflang-34127.html)
- [Yoast：hreflang 终极指南](https://yoast.com/hreflang-ultimate-guide/)

### Google 与 Bing

Bing 将 hreflang 视为"弱信号"。Bing 依赖 `content-language` meta 标签、HTML `lang` 属性、ccTLD 和服务器位置。Yandex 像 Google 一样支持 hreflang。

对于两个搜索引擎：实施 hreflang（Google/Yandex）+ `<html lang="...">` + `<meta http-equiv="content-language">`（Bing）。

- [Digital Ready Marketing：Bing 不使用 Hreflang](https://digitalreadymarketing.com/bing-doesnt-use-hreflang-annotation-what-does-it-use/)
- [Yoast：hreflang 终极指南](https://yoast.com/hreflang-ultimate-guide/)

---

## 规范化与国际化

### 自引用规范标签

每个语言环境页面必须规范到自身。John Mueller 表示："不要跨语言/国家使用 rel=canonical，仅在每个国家/语言基础上使用。"

Google 文档指出："指定相同语言的规范页面，或者如果不存在相同语言的规范页面，则指定最佳可能的替代语言。"

- [John Mueller：hreflang canonical](https://johnmu.com/hreflang-canonical/)
- [Google：合并重复的 URL](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls)

### 规范标签覆盖 Hreflang

Mueller 表示："如果您的规范标签指向其他地方，Google 将遵循该标签并忽略您的 hreflang 注释。"规范 URL 必须是 hreflang 集合中的 URL 之一，否则所有 hreflang 标记都会被忽略。

Google 还指出："Google 更喜欢作为 hreflang 集群一部分的 URL 进行规范化"——当信号一致时，hreflang 会加强规范选择。

- [John Mueller：hreflang canonical](https://johnmu.com/hreflang-canonical/)
- [SEJ：Hreflang 标签是提示](https://www.searchenginejournal.com/google-reminds-that-hreflang-tags-are-hints-not-directives/546428/)
- [Google：合并重复的 URL](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls)

### 近乎重复的地区变体

Mueller（2023 办公时间）："如果内容完全相同，我们无法区分任何差异，那么为了简单性和用户体验，我们可能只显示一个版本——即使存在 hreflang。"

Google 的重复检测在 hreflang 评估之前运行。要保持两个版本都被索引，您需要超出货币符号的实质性内容差异。

- [International Web Mastery：同语言重复页面](https://internationalwebmastery.com/blog/how-google-handles-canonicalization-of-same-language-duplicate-near-duplicate-pages/)
- [Google：管理多地区网站](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites)

### 跨语言环境的分页

Google 表示："不要将分页序列的第一页用作规范页面。相反，为每个页面提供自己的规范 URL。"每个语言环境中的每个分页页面都获得自引用规范标签。`rel="next/prev"` 已于 2019 年 3 月弃用。

- [Google：分页最佳实践](https://developers.google.com/search/docs/specialty/ecommerce/pagination-and-incremental-page-loading)

---

## 国际 Sitemap

### 结构

每个 `<url>` 条目包含每个语言环境的 `<xhtml:link>` 变体。需要 `xmlns:xhtml="http://www.w3.org/1999/xhtml"` 命名空间。

按内容类型拆分 sitemap，而不是按语言环境拆分。按语言环境拆分会造成维护问题，因为每个语言环境 sitemap 必须引用所有其他语言环境（互惠要求）。

- [Google Search Central：本地化版本](https://developers.google.com/search/docs/specialty/international/localized-versions)
- [Lumar：Google 如何处理 Hreflang](https://www.lumar.io/office-hours/hreflang/)

### 大小限制

每个 sitemap 50,000 URL / 50MB 未压缩。只有 `<loc>` 元素计入 50K 限制。但是，如果每个条目有 20 个 hreflang 变体，50MB 文件大小限制将成为瓶颈。使用完整 hreflang 时，计划每个 sitemap 容纳 2,000-5,000 个 URL。

- [Google：构建并提交 Sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap)
- [SERoundtable：Sitemap 50,000 限制](https://www.seroundtable.com/google-sitemap-50-000-limit-based-on-location-urls-not-alternative-urls-33843.html)

### 提交

在 Search Console 中提交 sitemap 索引并在 robots.txt 中引用它。可以单独提交各个子 sitemap 以获取每个 sitemap 的报告。

- [Google：构建并提交 Sitemap](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap)

### Next.js 注意事项

Next.js `alternates.languages` 不会自动为 `<loc>` URL 包含自引用的 `<xhtml:link>`。您必须在 `languages` 对象中显式包含 `<loc>` URL 自身的语言。

- [Next.js 文档：sitemap.xml](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/sitemap)

---

## URL 结构

### 策略比较

Google 同等对待子目录和子域名。Mueller 表示："从我们的角度来看……他们说子域名和子目录本质上是等效的。"

根据 Google 文档，URL 参数（`?lang=en`）被明确列为"不推荐"。

- [Google：管理多地区网站](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites)

### 默认语言

Mueller 建议：将 `/` 设置为 x-default，将每种语言放在自己的前缀中。如果不将 `/` 标记为 x-default，"对 Google 来说，'/' 看起来像是与其他页面不同的独立页面。"

- [Google Blog：x-default](https://developers.google.com/search/blog/2023/05/x-default)
- [Google Blog：为您的网站创建合适的主页](https://developers.google.com/search/blog/2014/05/creating-right-homepage-for-your)

### 内容协商 / IP 重定向

Google 强烈建议不要使用语言环境自适应页面。Googlebot 从美国 IP 爬取且不发送 Accept-Language 标头。需要单独的 URL + hreflang。

- [Google：语言环境自适应页面](https://developers.google.com/search/docs/specialty/international/locale-adaptive-pages)

### 尾部斜杠一致性

Mueller 表示：尾部斜杠是"URL 的重要组成部分，如果存在或不存在，将改变 URL。"为所有语言环境路径、内部链接、规范标签、hreflang 和 sitemap 选择一种格式。

Mueller（2025）："一致性是最大的技术 SEO 因素。"

- [SERoundtable：一致性是最大的技术 SEO 因素](https://www.seroundtable.com/google-consistency-seo-40427.html)

### Search Console 地理定位

国际定位报告已弃用。Google 现在完全依赖 hreflang、内容语言分析和链接模式。您可以添加子目录属性以获取每个语言环境的报告。

- [Google Support：国际定位已弃用](https://support.google.com/webmasters/answer/12474899?hl=en)

### 框架语言环境模式

使用 `localePrefix: 'always'`（next-intl）或等效配置。永远不要在 URL 中隐藏语言环境——Google 需要每种语言的唯一 URL。使用 `'never'` 模式会完全禁用备用链接。

- [next-intl：路由配置](https://next-intl.dev/docs/routing/configuration)
- [Next.js 讨论 #18419](https://github.com/vercel/next.js/discussions/18419)

---

## 跨语言环境的内容质量

### 自动翻译内容（2025 立场）

Google 在 2025 年年中去除了长期以来反对自动翻译内容的指导。当前立场："我们的政策并未严格定义由 AI 翻译的内容为垃圾内容。"规模化内容滥用政策提到翻译作为一种可能的载体，但并未禁止。

Reddit 在 Google 知情的情况下将 AI 翻译扩展到 35+ 种语言。关键区别在于意图和质量，而非方法。

- [Google 垃圾内容政策](https://developers.google.com/search/docs/essentials/spam-policies)
- [Glenn Gabe：自动翻译内容](https://www.gsqi.com/marketing-blog/auto-translating-content-google-scaled-content-abuse/)
- [SE Land：Reddit AI 翻译](https://searchengineland.com/google-comments-on-reddits-use-of-ai-to-translate-its-pages-456908)

### 薄弱的语言环境页面

Google 表示："只有当页面的主要内容保持未翻译状态时，页面的本地化版本才被视为重复。"仅翻译样板文字的页面会被聚类为重复内容。

不要对不需要的语言环境页面使用 noindex（浪费爬取预算）。不要跨语言环境使用规范标签（与 hreflang 冲突）。最佳方法：不要创建您无法使其真正有用的语言环境页面。

- [Google：本地化版本](https://developers.google.com/search/docs/specialty/international/localized-versions)
- [Google：爬取预算管理](https://developers.google.com/search/docs/crawling-indexing/large-site-managing-crawl-budget)

### 有用内容系统的影响

于 2024 年 3 月合并到核心排名中。全站信号："网站上相对大量无用内容的任何内容——不仅仅是无用内容——在搜索中表现不佳的可能性较低。"

低质量的翻译页面可能会拖累整个网站。这是反对创建并非真正有用的语言环境页面的最强有力论据。

- [Google Blog：有用内容更新](https://developers.google.com/search/blog/2022/08/helpful-content-update)
- [Amsive：2024 年的变化](https://www.amsive.com/insights/seo/googles-helpful-content-update-ranking-system-what-happened-and-what-changed-in-2024/)

### 部分翻译

Google 表示："仅翻译页面的样板文字而将大部分内容保留为单一语言……会造成糟糕的用户体验。"Google 使用可见内容（而非 lang 属性）来确定页面语言。

如果创建语言环境版本，请翻译页面上的所有内容。错误语言的未翻译元数据（标题、描述）会降低 CTR。

- [Google：管理多地区网站](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites)

### 爬取预算

仅对于 100 万+ 页面或每天 1 万+ 页面变化的网站才是问题。但是备用 URL（hreflang 目标）确实会消耗爬取预算。损坏的 hreflang 链接既浪费预算又使信号失效。

- [Google：爬取预算管理](https://developers.google.com/search/docs/crawling-indexing/large-site-managing-crawl-budget)
- [Google Blog：爬取预算](https://developers.google.com/search/blog/2017/01/what-crawl-budget-means-for-googlebot)

### 语言环境特定信号

Google 通过以下方式识别受众："页面上的本地地址和电话号码、使用当地语言和货币、来自其他本地网站的链接，或来自您的商家资料的信号。"

- [Google：管理多地区网站](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites)
