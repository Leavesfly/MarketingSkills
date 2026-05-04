# OneSignal

推送通知、邮件、短信和应用内消息平台，用于大规模客户互动。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | 通知、用户、细分、模板、应用 |
| MCP | - | 不可用 |
| CLI | ✓ | [onesignal.js](../clis/onesignal.js) |
| SDK | ✓ | JavaScript、Node.js、Python、Java、PHP、Ruby、Go、.NET |

## 身份验证

- **类型**：REST API Key（Basic Auth）
- **请求头**：`Authorization: Basic {REST_API_KEY}`
- **App ID**：在请求体中需要作为 `app_id`
- **获取凭证**：Dashboard > Settings > Keys & IDs
- **安全**：需要 HTTPS，端口 443 上使用 TLS 1.2+

## 常见 Agent 操作

### 向细分发送推送通知

```bash
POST https://api.onesignal.com/api/v1/notifications

Headers:
  Authorization: Basic {REST_API_KEY}
  Content-Type: application/json

{
  "app_id": "YOUR_APP_ID",
  "included_segments": ["Subscribed Users"],
  "headings": { "en": "New Feature!" },
  "contents": { "en": "Check out our latest update." },
  "url": "https://example.com/feature"
}
```

### 向特定用户发送通知

```bash
POST https://api.onesignal.com/api/v1/notifications

Headers:
  Authorization: Basic {REST_API_KEY}
  Content-Type: application/json

{
  "app_id": "YOUR_APP_ID",
  "include_aliases": { "external_id": ["user-123", "user-456"] },
  "target_channel": "push",
  "contents": { "en": "You have a new message." }
}
```

### 安排通知

```bash
POST https://api.onesignal.com/api/v1/notifications

Headers:
  Authorization: Basic {REST_API_KEY}
  Content-Type: application/json

{
  "app_id": "YOUR_APP_ID",
  "included_segments": ["Subscribed Users"],
  "contents": { "en": "Scheduled notification" },
  "send_after": "2025-12-01 12:00:00 GMT-0500"
}
```

### 列出通知

```bash
GET https://api.onesignal.com/api/v1/notifications?app_id={APP_ID}&limit=50&offset=0

Headers:
  Authorization: Basic {REST_API_KEY}
```

### 查看通知

```bash
GET https://api.onesignal.com/api/v1/notifications/{notification_id}?app_id={APP_ID}

Headers:
  Authorization: Basic {REST_API_KEY}
```

### 取消已安排的通知

```bash
DELETE https://api.onesignal.com/api/v1/notifications/{notification_id}?app_id={APP_ID}

Headers:
  Authorization: Basic {REST_API_KEY}
```

### 列出细分

```bash
GET https://api.onesignal.com/api/v1/apps/{APP_ID}/segments

Headers:
  Authorization: Basic {REST_API_KEY}
```

### 创建细分

```bash
POST https://api.onesignal.com/api/v1/apps/{APP_ID}/segments

Headers:
  Authorization: Basic {REST_API_KEY}
  Content-Type: application/json

{
  "name": "Active Users",
  "filters": [
    { "field": "session_count", "relation": ">", "value": "5" }
  ]
}
```

### 通过外部 ID 获取用户

```bash
GET https://api.onesignal.com/api/v1/apps/{APP_ID}/users/by/external_id/{external_id}

Headers:
  Authorization: Basic {REST_API_KEY}
```

### 创建用户

```bash
POST https://api.onesignal.com/api/v1/apps/{APP_ID}/users

Headers:
  Authorization: Basic {REST_API_KEY}
  Content-Type: application/json

{
  "identity": { "external_id": "user-789" },
  "subscriptions": [
    { "type": "Email", "token": "user@example.com" }
  ],
  "tags": { "plan": "pro", "signup_source": "organic" }
}
```

### 列出模板

```bash
GET https://api.onesignal.com/api/v1/templates?app_id={APP_ID}

Headers:
  Authorization: Basic {REST_API_KEY}
```

## 关键指标

### 通知指标
- `successful` - 成功投递数量
- `failed` - 失败投递数量
- `converted` - 点击/转化的用户数
- `remaining` - 仍在队列中的通知
- `errored` - 错误数量
- `opened` - 通知打开次数

### 用户指标
- `session_count` - 总会话数
- `last_active` - 最后活动时间戳
- `tags` - 自定义键值元数据
- `subscriptions` - 活跃订阅渠道

## 参数

### 通知参数
- `app_id` - 应用 ID（必填）
- `included_segments` - 目标细分数组
- `excluded_segments` - 排除的细分数组
- `include_aliases` - 通过别名定位特定用户
- `target_channel` - 渠道：`push`、`email`、`sms`
- `contents` - 按语言代码划分的消息内容
- `headings` - 按语言代码划分的通知标题
- `url` - 点击时启动的 URL
- `data` - 自定义键值数据负载
- `send_after` - 计划发送时间（UTC 字符串）
- `ttl` - 存活时间（秒）

### 细分过滤字段
- `session_count` - 会话数量
- `first_session` - 首次会话日期
- `last_session` - 最后会话日期
- `tag` - 自定义标签值
- `language` - 用户语言
- `app_version` - 应用版本
- `country` - 用户国家代码

## 使用场景

- 发送产品更新的推送通知
- 基于用户行为的触发式通知
- 多渠道消息（推送 + 邮件 + 短信）
- 针对非活跃用户的重新参与活动
- 细分用户以进行定向消息传递
- A/B 测试通知内容
- 安排促销活动

## 速率限制

- **免费套餐**：每个应用每秒 150 次通知请求
- **付费套餐**：每个应用每秒 6,000 次通知请求
- **用户/订阅操作**：每个应用每秒 1,000 次请求
- **突发限制**：15 分钟内不超过总订阅者数的 10 倍
- **429 响应**：包含 `RetryAfter` 请求头，指示等待秒数

## 相关 Skills

- push-notifications
- customer-engagement
- retention-campaign
- re-engagement
- lifecycle-marketing
