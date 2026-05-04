# Intercom

客户消息传递和支持平台 API，用于管理联系人、对话、消息、公司、文章和标签。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API v2.11+ - 联系人、对话、消息、公司、文章、标签 |
| MCP | - | 不可用 |
| CLI | ✓ | [intercom.js](../clis/intercom.js) |
| SDK | ✓ | Node.js、Ruby、Python、PHP、Go |

## 认证

- **类型**: Bearer Token（访问令牌或 OAuth 2.0）
- **请求头**: `Authorization: Bearer {token}`
- **版本请求头**: `Intercom-Version: 2.11`
- **获取密钥**: Developer Hub，地址 https://app.intercom.com/a/apps/_/developer-hub

## 常见 Agent 操作

### 列出联系人

```bash
GET https://api.intercom.io/contacts
```

### 获取联系人

```bash
GET https://api.intercom.io/contacts/{id}
```

### 创建联系人

```bash
POST https://api.intercom.io/contacts

{
  "role": "user",
  "email": "user@example.com",
  "name": "Jane Doe",
  "custom_attributes": {
    "plan": "pro"
  }
}
```

### 更新联系人

```bash
PUT https://api.intercom.io/contacts/{id}

{
  "name": "Jane Smith",
  "custom_attributes": {
    "plan": "enterprise"
  }
}
```

### 搜索联系人

```bash
POST https://api.intercom.io/contacts/search

{
  "query": {
    "field": "email",
    "operator": "=",
    "value": "user@example.com"
  }
}
```

### 删除联系人

```bash
DELETE https://api.intercom.io/contacts/{id}
```

### 列出对话

```bash
GET https://api.intercom.io/conversations
```

### 获取对话

```bash
GET https://api.intercom.io/conversations/{id}
```

### 搜索对话

```bash
POST https://api.intercom.io/conversations/search

{
  "query": {
    "field": "open",
    "operator": "=",
    "value": true
  }
}
```

### 回复对话

```bash
POST https://api.intercom.io/conversations/{id}/reply

{
  "message_type": "comment",
  "type": "admin",
  "admin_id": "{admin_id}",
  "body": "Thanks for reaching out!"
}
```

### 创建消息

```bash
POST https://api.intercom.io/messages

{
  "message_type": "inapp",
  "body": "Welcome to our platform!",
  "from": {
    "type": "admin",
    "id": "{admin_id}"
  },
  "to": {
    "type": "user",
    "id": "{user_id}"
  }
}
```

### 列出公司

```bash
GET https://api.intercom.io/companies
```

### 创建或更新公司

```bash
POST https://api.intercom.io/companies

{
  "company_id": "company_123",
  "name": "Acme Corp",
  "plan": "enterprise",
  "custom_attributes": {
    "industry": "Technology"
  }
}
```

### 列出标签

```bash
GET https://api.intercom.io/tags
```

### 创建标签

```bash
POST https://api.intercom.io/tags

{
  "name": "VIP Customer"
}
```

### 标记联系人

```bash
POST https://api.intercom.io/contacts/{contact_id}/tags

{
  "id": "{tag_id}"
}
```

### 列出文章

```bash
GET https://api.intercom.io/articles
```

### 创建文章

```bash
POST https://api.intercom.io/articles

{
  "title": "Getting Started Guide",
  "body": "<p>Welcome to our platform...</p>",
  "author_id": "{admin_id}",
  "state": "published"
}
```

### 列出管理员

```bash
GET https://api.intercom.io/admins
```

### 提交事件

```bash
POST https://api.intercom.io/events

{
  "event_name": "purchased-item",
  "created_at": 1706140800,
  "user_id": "user_123",
  "metadata": {
    "item_name": "Pro Plan",
    "price": 99.00
  }
}
```

## 关键指标

### 联系人数据
- `id` - 唯一联系人标识符
- `role` - user 或 lead
- `email` - 联系人邮箱
- `name` - 联系人姓名
- `created_at` / `updated_at` - 时间戳
- `last_seen_at` - 最后活动时间
- `custom_attributes` - 自定义数据字段
- `tags` - 已应用的标签
- `companies` - 关联的公司

### 对话数据
- `id` - 对话标识符
- `state` - open、closed、snoozed
- `open` - 布尔值开放状态
- `read` - 阅读状态
- `priority` - 优先级级别
- `statistics` - 响应时间、计数
- `conversation_parts` - 消息历史

## 参数

### 列出联系人
- `per_page` - 每页结果数（默认 50，最大 150）
- `starting_after` - 分页游标

### 列出对话
- `per_page` - 每页结果数（默认 20，最大 150）
- `starting_after` - 分页游标

### 搜索（联系人和对话）
- `query.field` - 搜索字段
- `query.operator` - 比较运算符（=、!=、>、<、~、IN、NIN）
- `query.value` - 搜索值
- `pagination.per_page` - 每页结果数
- `pagination.starting_after` - 下一页游标
- `sort.field` / `sort.order` - 排序配置

## 使用场景

- 管理客户联系人记录和细分
- 自动化客户消息传递和入职流程
- 监控和响应支持对话
- 跟踪客户事件和行为
- 构建自定义支持工作流
- 在平台之间同步客户数据

## 速率限制

- **默认**: 每个应用每分钟 10,000 次 API 调用
- **每个工作区**: 每分钟 25,000 次 API 调用
- 以 10 秒窗口分布（每 10 秒重置）
- 请求头：`X-RateLimit-Limit`、`X-RateLimit-Remaining`、`X-RateLimit-Reset`
- 超出时返回 HTTP 429

## 相关技能

- customer-onboarding
- customer-retention
- lead-generation
- customer-support
- in-app-messaging
