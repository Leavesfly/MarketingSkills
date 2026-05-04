# Adobe Analytics

企业级分析平台，用于跨渠道衡量和归因分析。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Reporting API 2.0、Data Insertion API |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | ✓ | AppMeasurement.js、Mobile SDKs、Launch |

## 认证

- **类型**: OAuth 2.0（Service Account JWT）
- **设置**: 在 Adobe Developer Console 中创建集成
- **请求头**: `Authorization: Bearer {access_token}`

## 常用 Agent 操作

### 获取报表套件信息

```bash
GET https://analytics.adobe.io/api/{company_id}/reportsuites

Authorization: Bearer {access_token}
x-api-key: {client_id}
```

### 获取维度

```bash
GET https://analytics.adobe.io/api/{company_id}/dimensions?rsid={report_suite_id}

Authorization: Bearer {access_token}
x-api-key: {client_id}
```

### 获取指标

```bash
GET https://analytics.adobe.io/api/{company_id}/metrics?rsid={report_suite_id}

Authorization: Bearer {access_token}
x-api-key: {client_id}
```

### 运行报表

```bash
POST https://analytics.adobe.io/api/{company_id}/reports

{
  "rsid": "{report_suite_id}",
  "globalFilters": [{
    "type": "dateRange",
    "dateRange": "2024-01-01T00:00:00/2024-01-31T23:59:59"
  }],
  "metricContainer": {
    "metrics": [
      {"id": "metrics/visits"},
      {"id": "metrics/pageviews"},
      {"id": "metrics/orders"}
    ]
  },
  "dimension": "variables/evar1"
}
```

### 获取细分

```bash
GET https://analytics.adobe.io/api/{company_id}/segments?rsid={report_suite_id}

Authorization: Bearer {access_token}
x-api-key: {client_id}
```

### 数据插入（服务器端）

```bash
POST https://{tracking_server}/b/ss/{report_suite_id}/0

<?xml version="1.0" encoding="UTF-8"?>
<request>
  <visitorID>user_123</visitorID>
  <events>event1</events>
  <eVar1>campaign_name</eVar1>
  <prop1>page_type</prop1>
</request>
```

## AppMeasurement.js

```javascript
// 初始化
var s = s_gi('report_suite_id');
s.trackingServer = 'metrics.example.com';

// 设置变量
s.pageName = 'Home Page';
s.channel = 'Marketing';
s.eVar1 = 'campaign_name';
s.events = 'event1';

// 跟踪页面浏览
s.t();

// 跟踪链接
s.tl(this, 'o', 'Button Click');
```

## 关键概念

- **Report Suite** - 数据容器
- **eVars** - 转化变量（持久化）
- **props** - 流量变量（命中级别）
- **Events** - 成功指标
- **Segments** - 用户/访问过滤器
- **Calculated Metrics** - 派生指标

## 常用维度

- `variables/page` - 页面名称
- `variables/evar1` - 自定义转化变量
- `variables/prop1` - 自定义流量变量
- `variables/marketingchannel` - 营销渠道
- `variables/referringdomain` - 引荐域名

## 常用指标

- `metrics/visits` - 访问次数
- `metrics/pageviews` - 页面浏览量
- `metrics/uniquevisitors` - 独立访客数
- `metrics/orders` - 订单数
- `metrics/revenue` - 收入

## 适用场景

- 企业级规模分析
- 跨渠道归因分析
- 与 Adobe Experience Cloud 集成
- 高级细分功能
- 数据仓库导出

## 速率限制

- 每个公司每秒 12 个请求
- 每分钟 120 个请求

## 相关技能

- analytics-tracking
- ab-test-setup
- paid-ads
