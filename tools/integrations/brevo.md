# Brevo

一体化营销平台（前身为 Sendinblue），提供电子邮件、短信和 WhatsApp 服务，包括联系人管理、营销活动和事务性消息功能。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API v3，支持联系人、营销活动、事务性邮件/短信 |
| MCP | - | 不可用 |
| CLI | ✓ | [brevo.js](../clis/brevo.js) |
| SDK | ✓ | Node.js、Python、PHP、Ruby、Java、C#、Go |

## 认证

- **类型**: API Key
- **请求头**: `api-key: {api_key}`
- **获取密钥**: 在 https://app.brevo.com/settings/keys/api 的 SMTP & API 设置中获取
- **注意**: API 密钥仅在创建时显示一次；请妥善保存。以前使用 `api.sendinblue.com` 作为基础 URL。

## 常用 Agent 操作

### 获取账户信息

```bash
GET https://api.brevo.com/v3/account
```

### 列出联系人

```bash
GET https://api.brevo.com/v3/contacts?limit=50&offset=0
```

### 按邮箱获取联系人

```bash
GET https://api.brevo.com/v3/contacts/user@example.com
```

### 创建联系人

```bash
POST https://api.brevo.com/v3/contacts

{
  "email": "user@example.com",
  "attributes": {
    "FIRSTNAME": "Jane",
    "LASTNAME": "Doe"
  },
  "listIds": [1, 2]
}
```

### 更新联系人

```bash
PUT https://api.brevo.com/v3/contacts/user@example.com

{
  "attributes": {
    "FIRSTNAME": "Updated"
  },
  "listIds": [3]
}
```

### 删除联系人

```bash
DELETE https://api.brevo.com/v3/contacts/user@example.com
```

### 导入联系人

```bash
POST https://api.brevo.com/v3/contacts/import

{
  "jsonBody": [
    { "email": "user1@example.com" },
    { "email": "user2@example.com" }
  ],
  "listIds": [1]
}
```

### 列出联系人列表

```bash
GET https://api.brevo.com/v3/contacts/lists?limit=50&offset=0
```

### 创建列表

```bash
POST https://api.brevo.com/v3/contacts/lists

{
  "name": "Newsletter Subscribers",
  "folderId": 1
}
```

### 将联系人添加到列表

```bash
POST https://api.brevo.com/v3/contacts/lists/{listId}/contacts/add

{
  "emails": ["user1@example.com", "user2@example.com"]
}
```

### 从列表中移除联系人

```bash
POST https://api.brevo.com/v3/contacts/lists/{listId}/contacts/remove

{
  "emails": ["user1@example.com"]
}
```

### 发送事务性邮件

```bash
POST https://api.brevo.com/v3/smtp/email

{
  "sender": {
    "name": "My App",
    "email": "noreply@example.com"
  },
  "to": [
    { "email": "user@example.com", "name": "Jane Doe" }
  ],
  "subject": "Order Confirmation",
  "htmlContent": "<html><body><p>Your order is confirmed.</p></body></html>"
}
```

### 列出电子邮件营销活动

```bash
GET https://api.brevo.com/v3/emailCampaigns?limit=50&offset=0&type=classic&status=sent
```

### 创建电子邮件营销活动

```bash
POST https://api.brevo.com/v3/emailCampaigns

{
  "name": "January Newsletter",
  "subject": "Monthly Update",
  "sender": { "name": "My Brand", "email": "news@example.com" },
  "htmlContent": "<html><body><p>Newsletter content</p></body></html>",
  "recipients": { "listIds": [1, 2] }
}
```

### 立即发送营销活动

```bash
POST https://api.brevo.com/v3/emailCampaigns/{campaignId}/sendNow
```

### 发送营销活动测试邮件

```bash
POST https://api.brevo.com/v3/emailCampaigns/{campaignId}/sendTest

{
  "emailTo": ["test@example.com"]
}
```

### 发送事务性短信

```bash
POST https://api.brevo.com/v3/transactionalSMS/sms

{
  "sender": "MyApp",
  "recipient": "+15551234567",
  "content": "Your verification code is 123456",
  "type": "transactional"
}
```

### 列出短信营销活动

```bash
GET https://api.brevo.com/v3/smsCampaigns?limit=50&offset=0
```

### 列出发件人

```bash
GET https://api.brevo.com/v3/senders
```

## API 模式

Brevo 使用标准 REST 风格，采用基于偏移量的分页（`limit` 和 `offset` 参数）。联系人属性使用大写字段名（FIRSTNAME、LASTNAME 等）。列表嵌套在联系人资源路径下。尽管基于 REST，事务性邮件使用 `/smtp/email` 端点。

## 关键指标

### 联系人的字段
- `email` - 电子邮件地址
- `attributes` - 自定义属性（FIRSTNAME、LASTNAME、SMS 等）
- `listIds` - 关联的列表 ID
- `emailBlacklisted` - 邮件退订状态
- `smsBlacklisted` - 短信退订状态
- `statistics` - 参与度统计（需展开）

### 营销活动指标
- `sent` - 总发送数
- `delivered` - 成功送达数
- `openRate` - 打开率百分比
- `clickRate` - 点击率百分比
- `unsubscribed` - 退订数量
- `hardBounces`、`softBounces` - 退回数量

### 事务性邮件响应
- `messageId` - 用于追踪的唯一消息标识符

## 参数

### 联系人参数
- `email` - 联系人邮箱地址
- `attributes` - 自定义属性的键值对象
- `listIds` - 要订阅的列表 ID 数组
- `unlinkListIds` - 要取消订阅的列表 ID 数组

### 营销活动参数
- `name` - 营销活动名称
- `subject` - 邮件主题行
- `sender` - 包含 `name` 和 `email` 的对象
- `htmlContent` / `textContent` - 邮件正文
- `recipients` - 包含 `listIds` 数组的对象
- `type` - classic 或 trigger

## 适用场景

- 多渠道营销（电子邮件 + 短信 + WhatsApp）
- 带追踪功能的事务性邮件发送
- 管理联系人和细分列表
- 创建和调度电子邮件营销活动
- 短信通知和营销
- 经济实惠的一体化营销自动化

## 速率限制

- API 速率限制取决于套餐（免费版：每天发送次数有限）
- 事务性邮件：根据套餐而异
- 联系人导入：批量处理，异步状态更新
- 响应中返回速率限制请求头

## 相关技能

- email-sequence
- sms-marketing
- transactional-email
- lifecycle-marketing
- contact-management
