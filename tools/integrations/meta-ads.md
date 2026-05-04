# Meta Ads (Facebook/Instagram)

用于 Facebook、Instagram、Messenger 和 Audience Network 的广告平台。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Marketing API，用于广告系列、受众群体、报告 |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | ✓ | Python、PHP、Node.js 官方 SDK |

## 身份验证

- **类型**：OAuth 2.0 Access Token
- **请求头**：Access token 作为查询参数
- **设置**：在 Meta Business Suite 中创建应用，生成 System User token

## 常见 Agent 操作

### 获取广告账户

```bash
GET https://graph.facebook.com/v18.0/me/adaccounts?access_token={access_token}&fields=id,name,account_status
```

### 获取广告系列

```bash
GET https://graph.facebook.com/v18.0/act_{ad_account_id}/campaigns?access_token={access_token}&fields=id,name,status,objective,daily_budget
```

### 获取广告系列洞察数据

```bash
GET https://graph.facebook.com/v18.0/{campaign_id}/insights?access_token={access_token}&fields=impressions,clicks,spend,actions,cost_per_action_type&date_preset=last_30d
```

### 获取广告组

```bash
GET https://graph.facebook.com/v18.0/act_{ad_account_id}/adsets?access_token={access_token}&fields=id,name,status,targeting,daily_budget,bid_amount
```

### 获取广告

```bash
GET https://graph.facebook.com/v18.0/{ad_set_id}/ads?access_token={access_token}&fields=id,name,status,creative
```

### 创建广告系列

```bash
POST https://graph.facebook.com/v18.0/act_{ad_account_id}/campaigns

access_token={access_token}
&name=Campaign Name
&objective=CONVERSIONS
&status=PAUSED
&special_ad_categories=[]
```

### 更新广告系列状态

```bash
POST https://graph.facebook.com/v18.0/{campaign_id}

access_token={access_token}
&status=ACTIVE
```

### 获取自定义受众群体

```bash
GET https://graph.facebook.com/v18.0/act_{ad_account_id}/customaudiences?access_token={access_token}&fields=id,name,approximate_count
```

### 创建相似受众群体

```bash
POST https://graph.facebook.com/v18.0/act_{ad_account_id}/customaudiences

access_token={access_token}
&name=Lookalike - Top Customers
&subtype=LOOKALIKE
&origin_audience_id={source_audience_id}
&lookalike_spec={"type":"similarity","country":"US"}
```

## 关键指标

| 指标 | 说明 |
|--------|-------------|
| `impressions` | 广告展示次数 |
| `clicks` | 所有点击 |
| `spend` | 花费金额 |
| `reach` | 触达的唯一用户数 |
| `frequency` | 每人平均展示次数 |
| `cpm` | 每千次展示成本 |
| `cpc` | 每次点击成本 |
| `actions` | 转化数组 |
| `cost_per_action_type` | 按行动类型的 CPA |

## 广告系列目标

- `AWARENESS` - 品牌知名度
- `TRAFFIC` - 网站流量
- `ENGAGEMENT` - 帖子互动
- `LEADS` - 潜在客户生成
- `APP_PROMOTION` - 应用安装
- `SALES` - 转化/目录销售

## 定向选项

```json
{
  "geo_locations": {
    "countries": ["US"],
    "cities": [{"key": "2420379"}]
  },
  "age_min": 25,
  "age_max": 45,
  "genders": [1, 2],
  "interests": [{"id": "6003139266461", "name": "Marketing"}],
  "behaviors": [{"id": "6002714895372"}]
}
```

## 使用场景

- 创建/管理 Facebook 和 Instagram 广告
- 受众群体定向和相似受众
- 广告系列效果分析
- 重定向设置

## 速率限制

- 每个广告账户每小时 200 次调用
- Marketing API 每小时 60 次调用
- 使用批量请求提高效率

## 相关 Skills

- paid-ads
- analytics-tracking
- page-cro
