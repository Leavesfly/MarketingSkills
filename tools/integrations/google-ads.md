# Google Ads

用于搜索、展示和视频广告的按点击付费广告平台。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Google Ads API，用于广告系列管理 |
| MCP | ✓ | 可通过 Google Ads MCP 服务器使用 |
| CLI | - | 使用 gcloud 或 API 脚本 |
| SDK | ✓ | 支持多种语言的客户端库 |

## 身份验证

- **类型**：OAuth 2.0
- **作用域**：`https://www.googleapis.com/auth/adwords`
- **设置**：在 Google Cloud Console 中创建凭据，关联到 Google Ads 账户
- **请求头**：`developer-token`、`login-customer-id`（适用于 MCC）

## 常见代理操作

### 获取账户信息

```bash
POST https://googleads.googleapis.com/v14/customers/{customer_id}/googleAds:searchStream

{
  "query": "SELECT customer.id, customer.descriptive_name FROM customer"
}
```

### 列出广告系列

```bash
POST https://googleads.googleapis.com/v14/customers/{customer_id}/googleAds:searchStream

{
  "query": "SELECT campaign.id, campaign.name, campaign.status, campaign_budget.amount_micros FROM campaign ORDER BY campaign.id"
}
```

### 获取广告系列效果

```bash
POST https://googleads.googleapis.com/v14/customers/{customer_id}/googleAds:searchStream

{
  "query": "SELECT campaign.name, metrics.impressions, metrics.clicks, metrics.cost_micros, metrics.conversions FROM campaign WHERE segments.date DURING LAST_30_DAYS"
}
```

### 获取广告组效果

```bash
POST https://googleads.googleapis.com/v14/customers/{customer_id}/googleAds:searchStream

{
  "query": "SELECT ad_group.name, metrics.impressions, metrics.clicks, metrics.conversions FROM ad_group WHERE segments.date DURING LAST_7_DAYS"
}
```

### 获取关键词效果

```bash
POST https://googleads.googleapis.com/v14/customers/{customer_id}/googleAds:searchStream

{
  "query": "SELECT ad_group_criterion.keyword.text, metrics.impressions, metrics.clicks, metrics.average_cpc FROM keyword_view WHERE segments.date DURING LAST_30_DAYS ORDER BY metrics.clicks DESC LIMIT 50"
}
```

### 暂停广告系列

```bash
POST https://googleads.googleapis.com/v14/customers/{customer_id}/campaigns:mutate

{
  "operations": [{
    "update": {
      "resourceName": "customers/{customer_id}/campaigns/{campaign_id}",
      "status": "PAUSED"
    },
    "updateMask": "status"
  }]
}
```

### 更新预算

```bash
POST https://googleads.googleapis.com/v14/customers/{customer_id}/campaignBudgets:mutate

{
  "operations": [{
    "update": {
      "resourceName": "customers/{customer_id}/campaignBudgets/{budget_id}",
      "amountMicros": "50000000"
    },
    "updateMask": "amountMicros"
  }]
}
```

## 关键指标

| 指标 | 说明 |
|--------|-------------|
| `metrics.impressions` | 广告展示次数 |
| `metrics.clicks` | 点击次数 |
| `metrics.cost_micros` | 费用（微单位，除以 1M） |
| `metrics.conversions` | 转化次数 |
| `metrics.conversions_value` | 转化价值 |
| `metrics.average_cpc` | 平均每次点击费用 |
| `metrics.ctr` | 点击率 |
| `metrics.conversion_rate` | 转化率 |

## 广告系列类型

- `SEARCH` - 搜索网络文字广告
- `DISPLAY` - 展示网络
- `SHOPPING` - 商品购物广告
- `VIDEO` - YouTube 视频广告
- `PERFORMANCE_MAX` - 跨渠道 AI 优化
- `DEMAND_GEN` - 发现/需求生成

## GAQL（Google Ads 查询语言）

```sql
SELECT
  campaign.name,
  metrics.clicks,
  metrics.conversions
FROM campaign
WHERE
  campaign.status = 'ENABLED'
  AND segments.date DURING LAST_30_DAYS
ORDER BY metrics.conversions DESC
LIMIT 10
```

## 使用时机

- 管理搜索广告系列
- 分析广告系列效果
- 调整预算和出价
- 关键词研究和管理
- 转化跟踪分析

## 速率限制

- 每天 15,000 次操作（基础版）
- 更高等级的开发者令牌可获得更高限制

## 相关技能

- paid-ads
- analytics-tracking
- page-cro
