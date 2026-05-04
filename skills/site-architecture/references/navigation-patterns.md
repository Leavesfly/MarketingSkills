# 导航模式

不同网站类型和上下文的详细导航模式。

---

## 头部导航

### 简单头部（4-6 个项目）

适用于：小企业、简单 SaaS、作品集。

```
[Logo]   Features   Pricing   Blog   About   [CTA Button]
```

规则：
- Logo 始终链接到首页
- CTA 按钮放在最右边，视觉上有区别（填充按钮、对比色）
- 项目按优先级排序（访问最多的在前）
- 活动页面获得视觉指示器（下划线、粗体、颜色）

### Mega Menu 头部

适用于：具有许多功能的 SaaS、具有类别的电子商务、大型内容网站。

```
[Logo]   Product ▾   Solutions ▾   Resources ▾   Pricing   Docs   [CTA]
```

当悬停/点击"Product"时：

```
┌─────────────────────────────────────────────────┐
│  Features           Platform        Integrations │
│  ─────────          ─────────       ──────────── │
│  Analytics           Security       Slack         │
│  Automation          API            HubSpot       │
│  Reporting           Compliance     Salesforce    │
│  Dashboards                         Zapier        │
│                                                   │
│  [See all features →]                             │
└─────────────────────────────────────────────────┘
```

Mega menu 规则：
- 最多 2-4 列
- 按逻辑分组项目（按功能区域、用例或受众）
- 在底部包含"查看全部"链接
- 不要在 mega menu 内嵌套下拉菜单
- 当标签本身不清楚时显示项目描述

### 分割导航

适用于：同时具有营销和产品导航的应用。

```
[Logo]   Features   Pricing   Blog        [Login]   [Sign Up]
├── Marketing nav (left) ──────┘          └── Auth nav (right) ──┤
```

右侧处理身份验证操作。左侧处理页面导航。

---

## 底部导航

### 基于列的底部（标准）

适用于：大多数网站。将链接组织成 3-5 个主题列。

```
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  Product          Resources        Company       Legal   │
│  ─────────        ──────────       ─────────     ─────   │
│  Features         Blog             About         Privacy │
│  Pricing          Guides           Careers       Terms   │
│  Integrations     Templates        Contact       GDPR    │
│  Changelog        Case Studies     Press                 │
│  Security         Webinars         Partners              │
│                                                          │
│  [Logo]  © 2026 Company Name                             │
│  Social: [Twitter] [LinkedIn] [GitHub]                   │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

### 极简底部

适用于：简单网站、落地页。

```
┌──────────────────────────────────────────────────────────┐
│  [Logo]                                                  │
│  © 2026 Company  ·  Privacy  ·  Terms  ·  Contact        │
└──────────────────────────────────────────────────────────┘
```

### 扩展底部

适用于：使用底部进行 SEO 的网站（比较页面、位置页面、资源链接）。

```
┌──────────────────────────────────────────────────────────┐
│  Product     Resources    Compare         Use Cases      │
│  Features    Blog         vs Competitor A  For Startups  │
│  Pricing     Guides       vs Competitor B  For Enterprise│
│  API         Templates    vs Competitor C  For Agencies  │
│                                                          │
│  Integrations             Popular Posts                  │
│  Slack       Zapier       How to Do X                    │
│  HubSpot     Salesforce   Guide to Y                     │
│                           Template: Z                    │
│                                                          │
│  [Logo]  © 2026  ·  Privacy  ·  Terms  ·  Security      │
└──────────────────────────────────────────────────────────┘
```

---

## 侧边栏导航

### 文档侧边栏

持久的左侧边栏，带有可折叠部分。

```
Getting Started
  ├── Installation
  ├── Quick Start
  └── Configuration

Guides
  ├── Authentication
  ├── Data Models
  └── Deployment

API Reference
  ├── REST API
  │   ├── Users
  │   ├── Projects
  │   └── Webhooks
  └── GraphQL

Examples
  ├── Next.js
  ├── Rails
  └── Python

Changelog
```

规则：
- 当前页面高亮显示
- 部分可折叠（活动部分默认展开）
- 侧边栏顶部有搜索
- 内容区域底部有"上一页/下一页"页面导航
- 滚动时固定（不会滚走）

### 博客分类侧边栏

```
Categories
  ├── SEO (24)
  ├── CRO (18)
  ├── Content (15)
  ├── Paid Ads (12)
  └── Analytics (9)

Popular Posts
  ├── How to Improve SEO
  ├── Landing Page Guide
  └── Analytics Setup

Newsletter
  └── [Email signup form]
```

---

## 面包屑导航

### 标准格式

```
Home > Features > Analytics
Home > Blog > SEO Category > How to Do Keyword Research
Home > Docs > API Reference > Authentication
```

规则：
- 分隔符：`>` 或 `/`（保持一致）
- 除当前页面外，每个段都是链接
- 当前页面是纯文本（未链接）
- 如果标题已作为 H1 可见，则不要包含当前页面

### 带 Schema 标记

```html
<nav aria-label="Breadcrumb">
  <ol itemscope itemtype="https://schema.org/BreadcrumbList">
    <li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem">
      <a itemprop="item" href="/"><span itemprop="name">Home</span></a>
      <meta itemprop="position" content="1" />
    </li>
    <li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem">
      <a itemprop="item" href="/features"><span itemprop="name">Features</span></a>
      <meta itemprop="position" content="2" />
    </li>
    <li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem">
      <span itemprop="name">Analytics</span>
      <meta itemprop="position" content="3" />
    </li>
  </ol>
</nav>
```

或使用 JSON-LD（推荐）：

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://example.com/" },
    { "@type": "ListItem", "position": 2, "name": "Features", "item": "https://example.com/features" },
    { "@type": "ListItem", "position": 3, "name": "Analytics" }
  ]
}
```

---

## 移动端导航

### 汉堡菜单

移动设备的标准。所有导航项目折叠到菜单图标中。

规则：
- 汉堡图标（三条线）右上角或左上角
- 全屏或滑出面板
- CTA 按钮无需打开菜单即可见（固定头部）
- 可从移动菜单访问搜索
- 嵌套项目的accordion模式

### 底部标签栏

适用于：Web 应用、PWA、移动优先产品。

```
┌──────────────────────────────────────┐
│                                      │
│           [Page Content]             │
│                                      │
├──────────────────────────────────────┤
│  Home    Search    Create    Profile │
│   🏠       🔍        ➕       👤    │
└──────────────────────────────────────┘
```

规则：
- 最多 3-5 个项目
- 图标 + 标签（不仅仅是图标）
- 活动状态清晰指示
- 最重要的操作在中间

---

## 反模式

### 要避免的事情

- **太多头部项目**（8+）：导致决策瘫痪，导航在小屏幕上变得不可读
- **下拉菜单嵌套**：下拉菜单内的下拉菜单内的下拉菜单
- **神秘图标**：没有标签的图标——用户不知道它们的含义
- **隐藏的主要导航**：在桌面上的汉堡菜单中埋没重要页面
- **页面间导航不一致**：导航在整个网站上应该相同（除了应用与营销）
- **没有移动考虑**：无法转换为移动的桌面导航
- **底部作为站点地图倾倒**：底部有 50+ 个链接且无组织
- **面包屑与 URL 不匹配**：面包屑说"Products > Widget"但 URL 是 `/shop/widget-pro`

### 常见修复

| 问题 | 修复 |
|---------|-----|
| 太多导航项目 | 分组为下拉菜单或 mega menu |
| 用户找不到页面 | 添加搜索，改进标签 |
| 导航跳出率高 | 简化选择，使用更清晰的标签 |
| SEO 页面未链接 | 添加到底部或资源部分 |
| 移动导航损坏 | 在实际设备上测试，使用汉堡模式 |

---

## SEO 导航

导航中的内部链接传递 PageRank。战略性地使用这一点：

- **头部导航链接最强**——将最重要的页面放在这里
- **底部链接传递较少价值**但仍然重要——适用于比较页面、位置页面
- **侧边栏链接**有助于版块级权威——适用于博客分类、文档部分
- **面包屑**向搜索引擎提供结构信号——使用 schema 标记实现
- **不要使用仅 JavaScript 的导航**——搜索引擎需要可爬取的 HTML 链接
- **使用描述性锚文本**——"Analytics Features"而不仅仅是"Features"
