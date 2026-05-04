# Google Analytics 4 (GA4)

用于跟踪用户行为、转化和营销表现的 Web 分析平台。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Data API 用于报告，Admin API 用于配置 |
| MCP | ✓ | 可通过 Google Analytics MCP 服务器使用 |
| CLI | - | 某些操作使用 gcloud |
| SDK | ✓ | gtag.js，Google Analytics 移动端 SDK |

## 身份验证

- **类型**：OAuth 2.0 或服务账号
- **作用域**：`https://www.googleapis.com/auth/analytics.readonly`（只读），`https://www.googleapis.com/auth/analytics.edit`（写入）
- **设置**：在 Google Cloud Console 中创建凭据

## 常见智能体操作

### 运行报告（Data API）

```bash
POST https://analyticsdata.googleapis.com/v1beta/properties/{property_id}:runReport

{
  "dateRanges": [{"startDate": "30daysAgo", "endDate": "today"}],
  "dimensions": [{"name": "sessionSource"}],
  "metrics": [{"name": "sessions"}, {"name": "conversions"}]
}
```

### 获取实时数据

```bash
POST https://analyticsdata.googleapis.com/v1beta/properties/{property_id}:runRealtimeReport

{
  "dimensions": [{"name": "country"}],
  "metrics": [{"name": "activeUsers"}]
}
```

### 列出转化事件

```bash
GET https://analyticsadmin.googleapis.com/v1beta/properties/{property_id}/conversionEvents
```

### 创建转化事件

```bash
POST https://analyticsadmin.googleapis.com/v1beta/properties/{property_id}/conversionEvents

{
  "eventName": "purchase"
}
```

## 客户端跟踪

### 发送自定义事件（gtag.js）

```javascript
gtag('event', 'signup_completed', {
  'method': 'email',
  'plan': 'free'
});
```

### 通过 Measurement Protocol 发送事件

```bash
POST https://www.google-analytics.com/mp/collect?measurement_id={measurement_id}&api_secret={api_secret}

{
  "client_id": "client_123",
  "events": [{
    "name": "purchase",
    "params": {
      "value": 99.99,
      "currency": "USD"
    }
  }]
}
```

## 关键维度与指标

### 常用维度
- `sessionSource` - 流量来源
- `sessionMedium` - 流量媒介
- `sessionCampaignName` - 活动名称
- `landingPage` - 入口页面
- `deviceCategory` - 设备类型
- `country` - 用户国家

### 常用指标
- `sessions` - 总会话数
- `activeUsers` - 活跃用户
- `newUsers` - 新用户
- `conversions` - 转化事件
- `engagementRate` - 参与会话率
- `averageSessionDuration` - 会话时长

## 何时使用

- 跟踪网站流量和用户行为
- 衡量营销活动表现
- 设置转化跟踪
- 分析用户旅程和漏斗
- 归因建模

## 速率限制

- Data API：每个属性每秒 10 次请求
- Admin API：因端点而异
- Measurement Protocol：免费层级每天 100 万次命中

## 相关技能

- analytics-tracking
- ab-test-setup
- seo-audit
- page-cro
