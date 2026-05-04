# Beehiiv

新闻通讯平台，提供订阅者管理、文章发布、自动化流程和推荐计划功能。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API v2，支持 publications、subscriptions、posts、segments |
| MCP | - | 不可用 |
| CLI | ✓ | [beehiiv.js](../clis/beehiiv.js) |
| SDK | - | 无官方 SDK；提供 OpenAPI 规范可用于代码生成 |

## 认证

- **类型**: Bearer Token
- **请求头**: `Authorization: Bearer {api_key}`
- **获取密钥**: 在 https://app.beehiiv.com 的 Workspace Settings > Settings > API 中获取
- **注意**: API 密钥仅在创建时显示一次；请立即复制并妥善保存

## 常用 Agent 操作

### 列出出版物

```bash
GET https://api.beehiiv.com/v2/publications
```

### 获取出版物详情

```bash
GET https://api.beehiiv.com/v2/publications/{publicationId}
```

### 列出订阅

```bash
GET https://api.beehiiv.com/v2/publications/{publicationId}/subscriptions?limit=10&status=active

# 按邮箱筛选
GET https://api.beehiiv.com/v2/publications/{publicationId}/subscriptions?email=user@example.com
```

### 创建订阅

```bash
POST https://api.beehiiv.com/v2/publications/{publicationId}/subscriptions

{
  "email": "user@example.com",
  "reactivate_existing": false,
  "send_welcome_email": true,
  "utm_source": "api",
  "tier": "free"
}
```

### 更新订阅

```bash
PUT https://api.beehiiv.com/v2/publications/{publicationId}/subscriptions/{subscriptionId}

{
  "tier": "premium"
}
```

### 删除订阅

```bash
DELETE https://api.beehiiv.com/v2/publications/{publicationId}/subscriptions/{subscriptionId}
```

### 列出文章

```bash
GET https://api.beehiiv.com/v2/publications/{publicationId}/posts?limit=10&status=confirmed
```

### 创建文章（仅限企业版）

```bash
POST https://api.beehiiv.com/v2/publications/{publicationId}/posts

{
  "title": "Weekly Update",
  "subtitle": "What happened this week",
  "content": "<p>Hello subscribers...</p>",
  "status": "draft"
}
```

### 列出细分群体

```bash
GET https://api.beehiiv.com/v2/publications/{publicationId}/segments
```

### 列出自动化流程

```bash
GET https://api.beehiiv.com/v2/publications/{publicationId}/automations
```

### 获取推荐计划

```bash
GET https://api.beehiiv.com/v2/publications/{publicationId}/referral_program
```

## API 模式

所有端点均限定于特定出版物。大多数操作需要将出版物 ID 作为必需的路径参数。响应使用基于游标的分页，通过 `cursor` 参数获取后续页面。

## 关键指标

### 订阅字段
- `status` - validating、invalid、pending、active、inactive
- `tier` - free 或 premium
- `created` - 订阅创建时间戳
- `utm_source`、`utm_medium`、`utm_campaign` - 获客追踪
- `referral_code` - 订阅者的唯一推荐码

### 文章字段
- `status` - draft、confirmed（已调度）、archived
- `publish_date` - 文章已发布或即将发布的时间
- `stats` - 打开率、点击率、订阅者数量（需展开）

## 参数

### 常用查询参数
- `limit` - 每页结果数（1-100，默认 10）
- `cursor` - 下一页结果的游标
- `expand[]` - 包含附加数据：stats、custom_fields、referrals
- `status` - 按订阅/文章状态筛选
- `tier` - 按订阅层级筛选（free、premium）

## 适用场景

- 以编程方式管理新闻通讯订阅者
- 从外部注册表单或落地页同步订阅者
- 构建推荐计划集成
- 自动化文章创建和发布工作流
- 追踪订阅者增长和参与度指标

## 速率限制

- API 速率限制按 API 密钥应用
- 使用基于游标的分页进行高效数据检索
- 不提供批量操作；需通过单个请求迭代处理

## 相关技能

- email-sequence
- newsletter-growth
- referral-program
- content-strategy
