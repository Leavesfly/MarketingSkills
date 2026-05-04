# ActiveCampaign

电子邮件营销自动化平台，提供 CRM、联系人管理、交易管道、标签、自动化流程和营销活动管理功能。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API v3，支持联系人、交易、自动化、营销活动、标签 |
| MCP | - | 不可用 |
| CLI | ✓ | [activecampaign.js](../clis/activecampaign.js) |
| SDK | ✓ | Python、PHP、Node.js、Ruby |

## 认证

- **类型**: API Token
- **请求头**: `Api-Token: {api_token}`
- **基础 URL**: `https://{yourAccountName}.api-us1.com/api/3`
- **获取密钥**: 在 ActiveCampaign 账户的设置 > Developer 选项卡中获取
- **注意**: 每个用户拥有唯一的 API 密钥。基础 URL 因账户而异（在设置 > Developer 中查找）。

## 常用 Agent 操作

### 获取当前用户

```bash
GET https://{account}.api-us1.com/api/3/users/me
```

### 列出联系人

```bash
GET https://{account}.api-us1.com/api/3/contacts?limit=20&offset=0

# 按邮箱搜索
GET https://{account}.api-us1.com/api/3/contacts?email=user@example.com

# 按姓名搜索
GET https://{account}.api-us1.com/api/3/contacts?search=Jane
```

### 创建联系人

```bash
POST https://{account}.api-us1.com/api/3/contacts

{
  "contact": {
    "email": "user@example.com",
    "firstName": "Jane",
    "lastName": "Doe",
    "phone": "+15551234567"
  }
}
```

### 更新联系人

```bash
PUT https://{account}.api-us1.com/api/3/contacts/{contactId}

{
  "contact": {
    "firstName": "Updated",
    "lastName": "Name"
  }
}
```

### 同步联系人（创建或更新）

```bash
POST https://{account}.api-us1.com/api/3/contact/sync

{
  "contact": {
    "email": "user@example.com",
    "firstName": "Jane",
    "lastName": "Doe"
  }
}
```

### 删除联系人

```bash
DELETE https://{account}.api-us1.com/api/3/contacts/{contactId}
```

### 列出所有列表

```bash
GET https://{account}.api-us1.com/api/3/lists?limit=20&offset=0
```

### 创建列表

```bash
POST https://{account}.api-us1.com/api/3/lists

{
  "list": {
    "name": "Newsletter",
    "stringid": "newsletter",
    "sender_url": "https://example.com",
    "sender_reminder": "You signed up for our newsletter."
  }
}
```

### 将联系人订阅到列表

```bash
POST https://{account}.api-us1.com/api/3/contactLists

{
  "contactList": {
    "list": "1",
    "contact": "1",
    "status": 1
  }
}
```

### 将联系人从列表取消订阅

```bash
POST https://{account}.api-us1.com/api/3/contactLists

{
  "contactList": {
    "list": "1",
    "contact": "1",
    "status": 2
  }
}
```

### 列出营销活动

```bash
GET https://{account}.api-us1.com/api/3/campaigns?limit=20&offset=0
```

### 列出交易

```bash
GET https://{account}.api-us1.com/api/3/deals?limit=20&offset=0

# 按管道阶段筛选
GET https://{account}.api-us1.com/api/3/deals?filters[stage]=1
```

### 创建交易

```bash
POST https://{account}.api-us1.com/api/3/deals

{
  "deal": {
    "title": "New Enterprise Deal",
    "value": 50000,
    "currency": "usd",
    "group": "1",
    "stage": "1",
    "owner": "1",
    "contact": "1"
  }
}
```

### 更新交易

```bash
PUT https://{account}.api-us1.com/api/3/deals/{dealId}

{
  "deal": {
    "stage": "2",
    "value": 75000
  }
}
```

### 列出自动化流程

```bash
GET https://{account}.api-us1.com/api/3/automations?limit=20&offset=0
```

### 将联系人添加到自动化流程

```bash
POST https://{account}.api-us1.com/api/3/contactAutomations

{
  "contactAutomation": {
    "contact": "1",
    "automation": "1"
  }
}
```

### 列出标签

```bash
GET https://{account}.api-us1.com/api/3/tags?limit=20&offset=0
```

### 创建标签

```bash
POST https://{account}.api-us1.com/api/3/tags

{
  "tag": {
    "tag": "VIP Customer",
    "tagType": "contact"
  }
}
```

### 为联系人添加标签

```bash
POST https://{account}.api-us1.com/api/3/contactTags

{
  "contactTag": {
    "contact": "1",
    "tag": "1"
  }
}
```

### 列出管道（交易组）

```bash
GET https://{account}.api-us1.com/api/3/dealGroups?limit=20&offset=0
```

### 列出 Webhook

```bash
GET https://{account}.api-us1.com/api/3/webhooks?limit=20&offset=0
```

### 创建 Webhook

```bash
POST https://{account}.api-us1.com/api/3/webhooks

{
  "webhook": {
    "name": "Contact Updated",
    "url": "https://example.com/webhook",
    "events": ["subscribe", "unsubscribe"],
    "sources": ["public", "admin", "api", "system"]
  }
}
```

## API 模式

ActiveCampaign 使用 REST 风格，资源采用包装格式（例如 `{ "contact": {...} }`）。响应包含资源对象及元数据。相关资源通过连接端点管理（例如 `/contactLists`、`/contactTags`、`/contactAutomations`）。基础 URL 因账户而异。分页使用 `limit` 和 `offset` 参数。

## 关键指标

### 联系人字段
- `email` - 电子邮件地址
- `firstName`、`lastName` - 姓名字段
- `phone` - 电话号码
- `cdate` - 创建日期
- `udate` - 最后更新日期
- `deals` - 关联交易数量

### 交易字段
- `title` - 交易名称
- `value` - 交易金额（以分为单位）
- `currency` - 货币代码
- `stage` - 管道阶段 ID
- `group` - 管道（交易组）ID
- `owner` - 分配的用户 ID
- `status` - 0（开放）、1（成交）、2（失败）

### 营销活动指标
- `sends` - 总发送数
- `opens` - 打开次数
- `clicks` - 点击次数
- `uniqueopens` - 独立打开数
- `uniquelinks` - 独立点击数

## 参数

### 联系人列表状态
- `1` - 已订阅（活跃）
- `2` - 已取消订阅

### 交易状态
- `0` - 开放
- `1` - 成交
- `2` - 失败

### 标签类型
- `contact` - 联系人标签
- `deal` - 交易标签

### 常用查询参数
- `limit` - 每页结果数（默认 20）
- `offset` - 跳过 N 条结果
- `search` - 文本搜索
- `email` - 按邮箱筛选联系人
- `filters[stage]` - 按阶段筛选交易
- `filters[owner]` - 按负责人筛选交易

## 适用场景

- 具有复杂条件工作流的营销自动化
- 带交易管道管理的 CRM
- 带标签和细分功能的联系人管理
- 电子邮件营销活动创建和跟踪
- 基于外部事件触发自动化流程
- B2B 销售管道跟踪与营销集成

## 速率限制

- 每个账户每秒 5 个请求
- 速率限制适用于同一账户下的所有 API 用户
- 429 响应包含 `Retry-After` 请求头

## 相关技能

- email-sequence
- lifecycle-marketing
- crm-integration
- sales-pipeline
- marketing-automation
