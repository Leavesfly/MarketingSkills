# 网站类型模板

常见网站类型的完整页面层级模板，包含 ASCII 树、URL 映射和导航建议。

---

## SaaS 营销网站

### 页面层级

```
首页 (/)
├── 功能 (/features)
│   ├── 功能 A (/features/feature-a)
│   ├── 功能 B (/features/feature-b)
│   └── 功能 C (/features/feature-c)
├── 定价 (/pricing)
├── 客户 (/customers)
│   ├── 案例研究 1 (/customers/company-name)
│   └── 案例研究 2 (/customers/company-name-2)
├── 资源 (/resources)
│   ├── 博客 (/blog)
│   │   └── [文章] (/blog/post-slug)
│   ├── 模板 (/resources/templates)
│   │   └── [模板] (/resources/templates/template-slug)
│   └── 指南 (/resources/guides)
│       └── [指南] (/resources/guides/guide-slug)
├── 集成 (/integrations)
│   └── [集成] (/integrations/integration-name)
├── 文档 (/docs)
│   ├── 入门指南 (/docs/getting-started)
│   ├── 指南 (/docs/guides)
│   └── API 参考 (/docs/api)
├── 关于 (/about)
│   ├── 招聘 (/about/careers)
│   └── 联系 (/contact)
├── 对比 (/compare)
│   └── [竞争对手] (/compare/competitor-name)
├── 隐私 (/privacy)
└── 条款 (/terms)
```

### URL 映射

| 页面 | URL | 导航位置 | 优先级 |
|------|-----|-------------|----------|
| 首页 | `/` | 头部（logo） | 关键 |
| 功能 | `/features` | 头部 | 高 |
| 功能页 | `/features/{slug}` | 头部落下拉菜单 | 中 |
| 定价 | `/pricing` | 头部 | 关键 |
| 客户 | `/customers` | 头部 | 中 |
| 案例研究 | `/customers/{slug}` | 客户下拉菜单 | 中 |
| 博客 | `/blog` | 头部（资源） | 高 |
| 博客文章 | `/blog/{slug}` | — | 中 |
| 集成 | `/integrations` | 头部 | 中 |
| 文档 | `/docs` | 头部 | 中 |
| 对比 | `/compare/{slug}` | 页脚 | 高（SEO） |
| 关于 | `/about` | 页脚 | 低 |
| 定价 CTA | `/pricing` | 头部（CTA 按钮） | 关键 |

### 导航

**头部（6 项 + CTA）**：功能 | 定价 | 客户 | 资源 | 集成 | 文档 | [开始使用]

**页脚列**：
- 产品：功能、定价、集成、更新日志、安全
- 资源：博客、模板、指南、案例研究
- 公司：关于、招聘、联系、新闻
- 法律：隐私、条款、安全

---

## 内容/博客网站

### 页面层级

```
首页 (/)
├── 博客 (/blog)
│   ├── [分类：主题 A] (/blog/category/topic-a)
│   ├── [分类：主题 B] (/blog/category/topic-b)
│   ├── [分类：主题 C] (/blog/category/topic-c)
│   └── [文章] (/blog/post-slug)
├── 通讯 (/newsletter)
├── 资源 (/resources)
│   ├── 指南 (/resources/guides)
│   │   └── [指南] (/resources/guides/guide-slug)
│   └── 工具 (/resources/tools)
│       └── [工具] (/resources/tools/tool-slug)
├── 关于 (/about)
├── 联系 (/contact)
├── 隐私 (/privacy)
└── 条款 (/terms)
```

### URL 映射

| 页面 | URL | 导航位置 | 优先级 |
|------|-----|-------------|----------|
| 首页 | `/` | 头部（logo） | 关键 |
| 博客索引 | `/blog` | 头部 | 高 |
| 分类 | `/blog/category/{slug}` | 头部落下拉菜单 | 中 |
| 文章 | `/blog/{slug}` | — | 中 |
| 通讯 | `/newsletter` | 头部（CTA） | 高 |
| 指南 | `/resources/guides` | 头部 | 中 |
| 关于 | `/about` | 头部 | 低 |

### 导航

**头部（4 项 + CTA）**：博客 | 资源 | 关于 | 联系 | [订阅]

**侧边栏**（在博客上）：分类、热门文章、通讯注册

---

## 电子商务

### 页面层级

```
首页 (/)
├── 商店 (/shop)
│   ├── 分类 A (/shop/category-a)
│   │   ├── 子分类 (/shop/category-a/subcategory)
│   │   │   └── [产品] (/shop/category-a/subcategory/product-slug)
│   │   └── [产品] (/shop/category-a/product-slug)
│   ├── 分类 B (/shop/category-b)
│   │   └── [产品] (/shop/category-b/product-slug)
│   └── 分类 C (/shop/category-c)
│       └── [产品] (/shop/category-c/product-slug)
├── 合集 (/collections)
│   └── [合集] (/collections/collection-slug)
├── 促销 (/sale)
├── 博客 (/blog)
│   └── [文章] (/blog/post-slug)
├── 关于 (/about)
│   └── 我们的故事 (/about/our-story)
├── 帮助 (/help)
│   ├── FAQ (/help/faq)
│   ├── 配送 (/help/shipping)
│   ├── 退货 (/help/returns)
│   └── 联系 (/contact)
├── 购物车 (/cart)
├── 账户 (/account)
├── 隐私 (/privacy)
└── 条款 (/terms)
```

### URL 映射

| 页面 | URL | 导航位置 | 优先级 |
|------|-----|-------------|----------|
| 首页 | `/` | 头部（logo） | 关键 |
| 商店 | `/shop` | 头部 | 关键 |
| 分类 | `/shop/{category}` | 头部 mega 菜单 | 高 |
| 产品 | `/shop/{category}/{product}` | — | 高 |
| 合集 | `/collections/{slug}` | 头部 | 中 |
| 促销 | `/sale` | 头部（突出显示） | 高 |
| 购物车 | `/cart` | 头部（图标） | 关键 |
| 账户 | `/account` | 头部（图标） | 中 |

### 导航

**头部（5 项 + 购物车/账户）**：商店（mega 菜单）| 合集 | 促销 | 博客 | 帮助 | [购物车图标] [账户图标]

**商店下的 Mega 菜单**：带有特色产品/图片的分类列

---

## 文档网站

### 页面层级

```
文档首页 (/docs)
├── 入门指南 (/docs/getting-started)
│   ├── 安装 (/docs/getting-started/installation)
│   ├── 快速开始 (/docs/getting-started/quick-start)
│   └── 配置 (/docs/getting-started/configuration)
├── 指南 (/docs/guides)
│   ├── 指南 A (/docs/guides/guide-a)
│   ├── 指南 B (/docs/guides/guide-b)
│   └── 指南 C (/docs/guides/guide-c)
├── API 参考 (/docs/api)
│   ├── 身份验证 (/docs/api/authentication)
│   ├── 端点 (/docs/api/endpoints)
│   └── Webhooks (/docs/api/webhooks)
├── 示例 (/docs/examples)
│   └── [示例] (/docs/examples/example-slug)
├── 更新日志 (/docs/changelog)
└── FAQ (/docs/faq)
```

### URL 映射

| 页面 | URL | 导航位置 | 优先级 |
|------|-----|-------------|----------|
| 文档首页 | `/docs` | 头部 | 高 |
| 入门指南 | `/docs/getting-started` | 侧边栏（顶部） | 关键 |
| 指南 | `/docs/guides` | 侧边栏 | 高 |
| API 参考 | `/docs/api` | 侧边栏 | 高 |
| 更新日志 | `/docs/changelog` | 侧边栏（底部） | 低 |

### 导航

**头部**：文档 | API | 博客 | 社区 | GitHub | [仪表板]

**侧边栏**（持久化，左侧）：入门指南、指南、API 参考、示例、更新日志 — 带有可展开的子部分

**页面内**：每个文档页面底部的上一个/下一个导航

---

## 混合 SaaS + 内容

### 页面层级

```
首页 (/)
├── 产品 (/product)
│   ├── 功能 A (/product/feature-a)
│   ├── 功能 B (/product/feature-b)
│   └── 功能 C (/product/feature-c)
├── 解决方案 (/solutions)
│   ├── 按用例 (/solutions/use-case-slug)
│   └── 按行业 (/solutions/industry-slug)
├── 定价 (/pricing)
├── 博客 (/blog)
│   ├── [分类] (/blog/category/slug)
│   └── [文章] (/blog/post-slug)
├── 资源 (/resources)
│   ├── 指南 (/resources/guides)
│   ├── 模板 (/resources/templates)
│   ├── 网络研讨会 (/resources/webinars)
│   └── 案例研究 (/resources/case-studies)
├── 文档 (/docs)
│   ├── 入门指南 (/docs/getting-started)
│   └── API (/docs/api)
├── 集成 (/integrations)
│   └── [集成] (/integrations/slug)
├── 对比 (/compare)
│   └── [竞争对手] (/compare/competitor-slug)
├── 关于 (/about)
│   ├── 招聘 (/about/careers)
│   └── 联系 (/contact)
├── 隐私 (/privacy)
└── 条款 (/terms)
```

### 导航

**头部（7 项 + CTA）**：产品 | 解决方案 | 定价 | 资源 | 博客 | 文档 | 集成 | [开始免费试用]

对产品（功能列表）、解决方案（用例 + 行业）和资源（博客、指南、模板、网络研讨会、案例研究）使用 mega 菜单。

---

## 小企业/本地

### 页面层级

```
首页 (/)
├── 服务 (/services)
│   ├── 服务 A (/services/service-a)
│   ├── 服务 B (/services/service-b)
│   └── 服务 C (/services/service-c)
├── 关于 (/about)
├── 推荐 (/testimonials)
├── 博客 (/blog)
│   └── [文章] (/blog/post-slug)
├── 联系 (/contact)
├── 隐私 (/privacy)
└── 条款 (/terms)
```

### URL 映射

| 页面 | URL | 导航位置 | 优先级 |
|------|-----|-------------|----------|
| 首页 | `/` | 头部（logo） | 关键 |
| 服务 | `/services` | 头部 | 高 |
| 服务页 | `/services/{slug}` | 头部落下拉菜单 | 高 |
| 关于 | `/about` | 头部 | 中 |
| 推荐 | `/testimonials` | 头部 | 中 |
| 博客 | `/blog` | 头部 | 中 |
| 联系 | `/contact` | 头部（CTA） | 高 |

### 导航

**头部（5 项 + CTA）**：服务 | 关于 | 推荐 | 博客 | [联系我们]

保持简单。小企业网站应该是扁平的（最多 1-2 层）。每个页面都应该可以从头部访问。
