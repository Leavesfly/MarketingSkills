# Google Search Console

用于监控网站搜索性能和索引状态的免费工具。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Search Analytics API、URL Inspection API |
| MCP | - | 不可用 |
| CLI | - | 使用 gcloud 或 API 脚本 |
| SDK | ✓ | Google API 客户端库 |

## 身份验证

- **类型**：OAuth 2.0 或服务账号
- **作用域**：`https://www.googleapis.com/auth/webmasters.readonly`
- **设置**：在 Google Cloud Console 中创建凭据

## 常见代理操作

### 获取搜索分析数据

```bash
POST https://searchconsole.googleapis.com/webmasters/v3/sites/{site_url}/searchAnalytics/query

{
  "startDate": "2024-01-01",
  "endDate": "2024-01-31",
  "dimensions": ["query"],
  "rowLimit": 100
}
```

### 按页面获取效果

```bash
POST https://searchconsole.googleapis.com/webmasters/v3/sites/{site_url}/searchAnalytics/query

{
  "startDate": "2024-01-01",
  "endDate": "2024-01-31",
  "dimensions": ["page"],
  "rowLimit": 50
}
```

### 按国家/地区获取效果

```bash
POST https://searchconsole.googleapis.com/webmasters/v3/sites/{site_url}/searchAnalytics/query

{
  "startDate": "2024-01-01",
  "endDate": "2024-01-31",
  "dimensions": ["country", "query"],
  "rowLimit": 100
}
```

### 检查 URL

```bash
POST https://searchconsole.googleapis.com/v1/urlInspection/index:inspect

{
  "inspectionUrl": "https://example.com/page",
  "siteUrl": "https://example.com/"
}
```

### 列出站点地图

```bash
GET https://searchconsole.googleapis.com/webmasters/v3/sites/{site_url}/sitemaps

Authorization: Bearer {access_token}
```

### 提交站点地图

```bash
PUT https://searchconsole.googleapis.com/webmasters/v3/sites/{site_url}/sitemaps/{sitemap_url}

Authorization: Bearer {access_token}
```

### 请求索引

```bash
POST https://indexing.googleapis.com/v3/urlNotifications:publish

{
  "url": "https://example.com/new-page",
  "type": "URL_UPDATED"
}
```

## 维度

- `query` - 搜索查询
- `page` - 页面 URL
- `country` - 国家/地区代码
- `device` - 设备类型（MOBILE、DESKTOP、TABLET）
- `date` - 日期
- `searchAppearance` - 搜索结果类型

## 指标

- `clicks` - 来自搜索的点击次数
- `impressions` - 搜索展示次数
- `ctr` - 点击率
- `position` - 平均排名

## 过滤器

```json
{
  "dimensionFilterGroups": [{
    "filters": [{
      "dimension": "query",
      "operator": "contains",
      "expression": "keyword"
    }]
  }]
}
```

## 使用时机

- 分析搜索效果
- 寻找关键词机会
- 监控索引状态
- 提交新页面进行索引
- 识别爬取问题
- 跟踪排名变化

## 速率限制

- 每分钟 200 次查询
- 每分钟 1,200 次请求

## 相关技能

- seo-audit
- programmatic-seo
- analytics-tracking
