# Close

面向中小企业的销售 CRM,内置电话、电子邮件和管道管理,专为高速销售团队设计。

## 能力

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Leads、Contacts、Opportunities、Activities、Tasks |
| MCP | - | 不可用 |
| CLI | ✓ | [close.js](../clis/close.js) |
| SDK | - | 仅 REST API |

## 认证

- **类型**: Basic Auth
- **请求头**: `Authorization: Basic {base64(api_key + ':')}`
- **获取密钥**: Settings > API Keys,访问 https://app.close.com

## 常见 Agent 操作

### 列出 Leads

```bash
GET https://api.close.com/api/v1/lead/

Authorization: Basic {base64(api_key + ':')}
```

### 搜索 Leads

```bash
GET https://api.close.com/api/v1/lead/?query=company_name

Authorization: Basic {base64(api_key + ':')}
```

### 创建 Lead

```bash
POST https://api.close.com/api/v1/lead/

{
  "name": "Acme Corp",
  "url": "https://acme.com",
  "description": "Enterprise prospect"
}
```

### 获取联系人

```bash
GET https://api.close.com/api/v1/contact/{contact_id}/

Authorization: Basic {base64(api_key + ':')}
```

### 创建联系人

```bash
POST https://api.close.com/api/v1/contact/

{
  "lead_id": "lead_xxx",
  "name": "Jane Smith",
  "emails": [{ "email": "jane@acme.com", "type": "office" }],
  "phones": [{ "phone": "+15551234567", "type": "office" }]
}
```

### 创建 Opportunity

```bash
POST https://api.close.com/api/v1/opportunity/

{
  "lead_id": "lead_xxx",
  "value": 50000,
  "status_type": "active"
}
```

### 列出 Activities

```bash
GET https://api.close.com/api/v1/activity/?lead_id=lead_xxx

Authorization: Basic {base64(api_key + ':')}
```

### 创建任务

```bash
POST https://api.close.com/api/v1/task/

{
  "lead_id": "lead_xxx",
  "text": "Follow up on demo request",
  "_type": "lead",
  "date": "2026-03-10"
}
```

## 关键指标

### Lead 数据
- `id` - Lead ID
- `display_name` - Lead 名称
- `url` - 网站 URL
- `description` - Lead 描述
- `status_id` - 管道状态
- `contacts` - 关联的联系人
- `opportunities` - 关联的 Opportunities
- `tasks` - 关联的任务

### 联系人数据
- `id` - 联系人 ID
- `lead_id` - 父级 lead
- `name` - 全名
- `title` - 职位头衔
- `emails` - 电子邮件地址数组
- `phones` - 电话号码数组

### Opportunity 数据
- `id` - Opportunity ID
- `lead_id` - 父级 lead
- `value` - 价值(以分为单位)
- `status_type` - active、won 或 lost
- `confidence` - 获胜概率(0-100)
- `date_won` - 成交日期

### 任务数据
- `id` - 任务 ID
- `lead_id` - 父级 lead
- `text` - 任务描述
- `assigned_to` - 分配的用户 ID
- `date` - 截止日期
- `is_complete` - 完成状态

## 参数

### Leads
- `query` - 搜索查询字符串
- `_skip` - 要跳过的结果数(分页)
- `_limit` - 返回的最大结果数(默认: 100)
- `_fields` - 要返回的逗号分隔字段

### Contacts
- `lead_id` - 按父级 lead 过滤
- `_skip` - 分页偏移量
- `_limit` - 最大结果数

### Opportunities
- `lead_id` - 按父级 lead 过滤
- `status` - 按状态类型过滤(active、won、lost)
- `_skip` - 分页偏移量
- `_limit` - 最大结果数

### Activities
- `lead_id` - 按 lead 过滤
- `_type__type` - 按类型过滤(Email、Call、Note、SMS、Meeting)
- `date_created__gt` - 指定日期之后
- `date_created__lt` - 指定日期之前

### Tasks
- `assigned_to` - 按用户 ID 过滤
- `is_complete` - 按完成状态过滤(true/false)
- `lead_id` - 按 lead 过滤
- `_type` - 任务类型(lead)

## 何时使用

- 管理需要高接触外联的中小企业销售管道
- 跟踪每个 lead 的销售活动(电话、电子邮件、会议)
- 创建和管理销售跟进任务
- Opportunity 跟踪和收入预测
- 构建自动化外联工作流
- 销售团队绩效报告

## 速率限制

- 速率限制基于组织计划
- 标准: 约 100 请求/分钟
- 响应包含 `ratelimit-limit` 和 `ratelimit-remaining` 请求头
- 429 响应包含 `Retry-After` 请求头

## 相关技能

- revops
- sales-enablement
- cold-email
