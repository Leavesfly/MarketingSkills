# Calendly

日程安排和预订平台 API，用于管理事件类型、已安排事件、受邀者和可用时间。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API v2 - 事件类型、已安排事件、受邀者、可用时间 |
| MCP | - | 不可用 |
| CLI | ✓ | [calendly.js](../clis/calendly.js) |
| SDK | ✓ | 无官方 SDK；有社区库可用 |

## 认证

- **类型**: Bearer Token（个人访问令牌或 OAuth 2.0）
- **请求头**: `Authorization: Bearer {token}`
- **获取密钥**: https://calendly.com/integrations/api_webhooks（个人访问令牌）

## 常用 Agent 操作

### 获取当前用户

```bash
GET https://api.calendly.com/users/me
```

### 列出事件类型

```bash
GET https://api.calendly.com/event_types?user={user_uri}
```

### 列出已安排事件

```bash
GET https://api.calendly.com/scheduled_events?user={user_uri}&min_start_time=2024-01-01T00:00:00Z&max_start_time=2024-12-31T23:59:59Z&status=active
```

### 获取已安排事件

```bash
GET https://api.calendly.com/scheduled_events/{event_uuid}
```

### 列出事件的受邀者

```bash
GET https://api.calendly.com/scheduled_events/{event_uuid}/invitees
```

### 取消已安排事件

```bash
POST https://api.calendly.com/scheduled_events/{event_uuid}/cancellation

{
  "reason": "Cancellation reason"
}
```

### 获取可用时间

```bash
GET https://api.calendly.com/event_type_available_times?event_type={event_type_uri}&start_time=2024-01-20T00:00:00Z&end_time=2024-01-27T00:00:00Z
```

### 获取用户忙碌时间

```bash
GET https://api.calendly.com/user_busy_times?user={user_uri}&start_time=2024-01-20T00:00:00Z&end_time=2024-01-27T00:00:00Z
```

### 列出组织成员

```bash
GET https://api.calendly.com/organization_memberships?organization={organization_uri}
```

### 创建 Webhook 订阅

```bash
POST https://api.calendly.com/webhook_subscriptions

{
  "url": "https://example.com/webhook",
  "events": ["invitee.created", "invitee.canceled"],
  "organization": "{organization_uri}",
  "scope": "organization"
}
```

### 列出 Webhook 订阅

```bash
GET https://api.calendly.com/webhook_subscriptions?organization={organization_uri}&scope=organization
```

### 删除 Webhook 订阅

```bash
DELETE https://api.calendly.com/webhook_subscriptions/{webhook_uuid}
```

## 关键指标

### 已安排事件数据
- `uri` - 唯一事件 URI
- `name` - 事件类型名称
- `status` - 事件状态（active、canceled）
- `start_time` / `end_time` - 事件时间
- `event_type` - 事件类型的 URI
- `location` - 会议位置详情
- `invitees_counter` - 受邀者数量（active、limit、total）

### 受邀者数据
- `name` - 受邀者全名
- `email` - 受邀者邮箱
- `status` - active 或 canceled
- `questions_and_answers` - 自定义问题回答
- `tracking` - UTM 参数
- `created_at` / `updated_at` - 时间戳

## 参数

### 列出已安排事件
- `user` - 用户 URI（必需）
- `min_start_time` / `max_start_time` - 日期范围筛选（ISO 8601）
- `status` - 按状态筛选（active、canceled）
- `count` - 结果数量（默认 20，最大 100）
- `page_token` - 分页令牌
- `sort` - 排序顺序（start_time:asc 或 start_time:desc）

### 列出事件类型
- `user` - 用户 URI
- `organization` - 组织 URI
- `active` - 筛选激活/未激活
- `count` - 每页结果数
- `sort` - 排序顺序

## 适用场景

- 检索已安排的会议数据以同步 CRM
- 监控预订活动和转化率
- 自动化会议后的跟进工作流
- 在建议会议时间前检查可用性
- 追踪会议取消和缺席情况
- 构建自定义预订界面

## 速率限制

- 未正式文档化；实施带指数退避的重试逻辑
- 使用保守的请求速率（避免突发请求）
- 监控 HTTP 429 响应

## 相关技能

- lead-generation
- sales-automation
- customer-onboarding
- appointment-scheduling
