# DataForSEO

全面的 SEO 数据 API，提供 SERP 结果、关键词研究、反向链接和页面分析功能。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | SERP、关键词数据、反向链接、页面分析、Labs |
| MCP | - | 不可用 |
| CLI | ✓ | [dataforseo.js](../clis/dataforseo.js) |
| SDK | ✓ | Python、TypeScript、PHP、Java、C# |

## 认证

- **类型**：Basic Auth
- **请求头**：`Authorization: Basic {base64(login:password)}`
- **获取凭证**：在 https://app.dataforseo.com/api-access 的 API Access 标签页
- **注意**：API 密码是自动生成的，与账户密码不同

## 常用 Agent 操作

### SERP - Google 自然搜索（实时）

```bash
POST https://api.dataforseo.com/v3/serp/google/organic/live/regular

[{
  "keyword": "marketing automation",
  "location_name": "United States",
  "language_name": "English"
}]
```

### 关键词 - 搜索量（实时）

```bash
POST https://api.dataforseo.com/v3/keywords_data/google_ads/search_volume/live

[{
  "keywords": ["email marketing", "marketing automation", "crm software"],
  "location_code": 2840,
  "language_code": "en"
}]
```

### 关键词 - 网站关键词（实时）

```bash
POST https://api.dataforseo.com/v3/keywords_data/google_ads/keywords_for_site/live

[{
  "target": "example.com",
  "location_code": 2840,
  "language_code": "en"
}]
```

### 反向链接 - 摘要

```bash
POST https://api.dataforseo.com/v3/backlinks/summary/live

[{
  "target": "example.com",
  "internal_list_limit": 10,
  "backlinks_status_type": "live"
}]
```

### 反向链接 - 列表

```bash
POST https://api.dataforseo.com/v3/backlinks/backlinks/live

[{
  "target": "example.com",
  "mode": "as_is",
  "limit": 100,
  "backlinks_status_type": "live"
}]
```

### 反向链接 - 引用域名

```bash
POST https://api.dataforseo.com/v3/backlinks/referring_domains/live

[{
  "target": "example.com",
  "limit": 100
}]
```

### 反向链接 - 索引（数据库统计）

```bash
GET https://api.dataforseo.com/v3/backlinks/index
```

### 页面分析 - 即时页面审计

```bash
POST https://api.dataforseo.com/v3/on_page/instant_pages

[{
  "url": "https://example.com/page",
  "enable_javascript": true
}]
```

### SERP - 位置列表

```bash
GET https://api.dataforseo.com/v3/serp/google/locations
```

### SERP - 语言列表

```bash
GET https://api.dataforseo.com/v3/serp/google/languages
```

## API 模式

DataForSEO 对大多数端点使用两种方法：
- **Live**（`/live`）- 同步，结果在同一响应中返回
- **任务式**（`/task_post` + `/task_get/$id`）- 异步，适用于大型请求

请求体始终是 JSON 数组（即使是单个请求）。

## 关键指标

### 关键词指标
- `search_volume` - 月搜索量
- `competition` - 竞争程度（0-1）
- `cpc` - 每次点击费用
- `monthly_searches` - 月度细分数组

### 反向链接指标
- `total_backlinks` - 反向链接总数
- `referring_domains` - 唯一引用域名数
- `domain_rank` - 域名权威分数
- `backlinks_spam_score` - 垃圾邮件分数

## 使用时机

- 大规模程序化 SERP 跟踪
- 带搜索量数据的关键词研究
- 反向链接分析和监控
- 页面 SEO 审计
- 竞争对手分析

## 速率限制

- 速率限制请求头：`X-RateLimit-Limit`、`X-RateLimit-Remaining`
- 反向链接 API：2000 请求/分钟，30 个并发
- 因端点和套餐而异

## 相关 Skills

- seo-audit
- programmatic-seo
- content-strategy
- competitor-alternatives
