# Demio

网络研讨会平台，用于举办直播、自动化和点播网络研讨会，内置注册和参会者跟踪功能。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | 活动、注册、参会者、会话 |
| MCP | - | 不可用 |
| CLI | ✓ | [demio.js](../clis/demio.js) |
| SDK | ✓ | PHP（官方）、Ruby（社区） |

## 认证

- **类型**：API Key + API Secret
- **请求头**：`Api-Key: {key}` 和 `Api-Secret: {secret}`
- **获取凭证**：账户设置 > API（需要所有者权限）
- **文档**：https://publicdemioapi.docs.apiary.io/

## 常用 Agent 操作

### Ping（健康检查）

```bash
GET https://my.demio.com/api/v1/ping

Headers:
  Api-Key: {API_KEY}
  Api-Secret: {API_SECRET}
```

### 列出所有活动

```bash
GET https://my.demio.com/api/v1/events

Headers:
  Api-Key: {API_KEY}
  Api-Secret: {API_SECRET}
```

### 按类型列出活动

```bash
GET https://my.demio.com/api/v1/events?type=upcoming

Headers:
  Api-Key: {API_KEY}
  Api-Secret: {API_SECRET}
```

### 获取特定活动

```bash
GET https://my.demio.com/api/v1/event/{event_id}

Headers:
  Api-Key: {API_KEY}
  Api-Secret: {API_SECRET}
```

### 获取活动日期详情

```bash
GET https://my.demio.com/api/v1/event/{event_id}/date/{date_id}

Headers:
  Api-Key: {API_KEY}
  Api-Secret: {API_SECRET}
```

### 为活动注册参会者

```bash
POST https://my.demio.com/api/v1/event/register

Headers:
  Api-Key: {API_KEY}
  Api-Secret: {API_SECRET}
  Content-Type: application/json

{
  "id": 12345,
  "name": "Jane Doe",
  "email": "jane@example.com"
}
```

### 为特定日期注册参会者

```bash
POST https://my.demio.com/api/v1/event/register

Headers:
  Api-Key: {API_KEY}
  Api-Secret: {API_SECRET}
  Content-Type: application/json

{
  "id": 12345,
  "date_id": 67890,
  "name": "Jane Doe",
  "email": "jane@example.com"
}
```

### 获取活动日期的参会者

```bash
GET https://my.demio.com/api/v1/date/{date_id}/participants

Headers:
  Api-Key: {API_KEY}
  Api-Secret: {API_SECRET}
```

## API 模式

Demio 使用简单的 REST API：
- 所有请求都需要 `Api-Key` 和 `Api-Secret` 请求头
- 响应是 JSON 对象
- 注册返回参会者的 `join_link` URL
- 活动有多个"日期"（会话），每个都有唯一的 `date_id`

## 关键指标

### 活动指标
- `id` - 活动 ID
- `name` - 活动名称
- `date_id` - 会话/日期标识符
- `status` - 活动状态（即将开始、已结束、进行中）
- `type` - 活动类型（直播、自动化、点播）
- `registration_url` - 公开注册页面 URL

### 参会者指标
- `name` - 参会者姓名
- `email` - 参会者邮箱
- `status` - 出席状态（已注册、已出席、缺席）
- `attended_minutes` - 出席时长
- `join_link` - 参会者的唯一加入链接

## 参数

### 活动列表过滤器
- `type` - 按活动类型过滤：`upcoming`、`past`、`all`

### 注册字段
- `id` - 活动 ID（必填）
- `name` - 注册人姓名（必填）
- `email` - 注册人邮箱（必填）
- `date_id` - 特定会话日期 ID（可选）
- `ref_url` - 用于跟踪的推荐 URL（可选）

### 自定义字段
- 自定义字段通过其 UID 支持（而非显示名称）
- 检查活动设置以获取可用的自定义字段 UID

## 使用时机

- 从落地页或表单自动化网络研讨会注册
- 将网络研讨会参会者数据同步到 CRM
- 为网络研讨会构建自定义注册流程
- 跟踪网络研讨会出席情况和参与度
- 根据出席状态触发后续序列
- 以编程方式管理多个网络研讨会会话

## 速率限制

- **每分钟 180 次请求**（每秒 3 次）
- **免费试用**：每天 100 次 API 调用
- **付费套餐**：每天 5,000 次 API 调用（UTC 00:00 重置）
- 联系 Demio 申请更高的每日限额
- 超出限制会返回错误响应

## 相关 Skills

- webinar-marketing
- lead-generation
- event-marketing
- content-strategy
- lifecycle-marketing
