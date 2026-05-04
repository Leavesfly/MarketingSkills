# Customer.io

基于行为的消息传递平台,支持电子邮件、推送通知、SMS 和应用内消息。

## 能力

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Track API、App API、Journeys API |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | ✓ | JavaScript、iOS、Android、Ruby、Python |

## 认证

- **Track API**: Site ID + API Key(Basic auth)
- **App API**: Bearer token
- **请求头**: `Authorization: Basic {base64(site_id:api_key)}`

## 常见 Agent 操作

### 识别客户

```bash
PUT https://track.customer.io/api/v1/customers/{customer_id}

Authorization: Basic {base64(site_id:api_key)}

{
  "email": "user@example.com",
  "created_at": 1705312800,
  "first_name": "John",
  "plan": "pro"
}
```

### 跟踪事件

```bash
POST https://track.customer.io/api/v1/customers/{customer_id}/events

Authorization: Basic {base64(site_id:api_key)}

{
  "name": "purchase",
  "data": {
    "product": "Pro Plan",
    "amount": 99
  }
}
```

### 跟踪匿名事件

```bash
POST https://track.customer.io/api/v1/events

Authorization: Basic {base64(site_id:api_key)}

{
  "name": "page_viewed",
  "data": {
    "page": "/pricing"
  },
  "anonymous_id": "anon_123"
}
```

### 删除客户

```bash
DELETE https://track.customer.io/api/v1/customers/{customer_id}

Authorization: Basic {base64(site_id:api_key)}
```

### 获取客户(App API)

```bash
GET https://api.customer.io/v1/customers/{customer_id}/attributes

Authorization: Bearer {app_api_key}
```

### 列出活动

```bash
GET https://api.customer.io/v1/campaigns

Authorization: Bearer {app_api_key}
```

### 获取活动指标

```bash
GET https://api.customer.io/v1/campaigns/{campaign_id}/metrics

Authorization: Bearer {app_api_key}
```

### 触发广播

```bash
POST https://api.customer.io/v1/campaigns/{campaign_id}/triggers

Authorization: Bearer {app_api_key}

{
  "emails": ["user@example.com"],
  "data": {
    "coupon_code": "SAVE20"
  }
}
```

### 发送事务性电子邮件

```bash
POST https://api.customer.io/v1/send/email

Authorization: Bearer {app_api_key}

{
  "transactional_message_id": "1",
  "to": "user@example.com",
  "identifiers": {
    "id": "user_123"
  },
  "message_data": {
    "order_id": "ORD-456"
  }
}
```

## JavaScript SDK

```javascript
// 初始化
_cio.identify({
  id: 'user_123',
  email: 'user@example.com',
  created_at: 1705312800,
  plan: 'pro'
});

// 跟踪事件
_cio.track('purchase', {
  product: 'Pro Plan',
  amount: 99
});

// 跟踪页面浏览
_cio.page();
```

## 关键概念

- **People** - 客户和潜在客户
- **Segments** - 基于属性/行为的动态群组
- **Campaigns** - 自动化消息序列
- **Broadcasts** - 一次性发送
- **Transactional** - 触发式消息

## 属性类型

- 标准:`email`、`created_at`、`unsubscribed`
- 自定义:你定义的任何键
- 计算:来自事件的聚合

## 何时使用

- 基于行为的电子邮件自动化
- 多渠道消息传递(电子邮件、推送、SMS)
- 入职序列
- 重新参与活动
- 事务性消息

## 速率限制

- Track API: 100 请求/秒
- App API: 10 请求/秒

## 相关技能

- email-sequence
- onboarding-cro
- analytics-tracking
