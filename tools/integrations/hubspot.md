# HubSpot

用于营销、销售和客户服务 CRM 平台。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API，用于 CRM、营销、销售 |
| MCP | - | 不可用 |
| CLI | ✓ | `hs` CLI，用于本地开发 |
| SDK | ✓ | 官方客户端库 |

## 身份验证

- **类型**：Private App Token 或 OAuth 2.0
- **请求头**：`Authorization: Bearer {access_token}`
- **获取令牌**：Settings > Integrations > Private Apps

## 常见代理操作

### 获取联系人

```bash
GET https://api.hubapi.com/crm/v3/objects/contacts?limit=10

Authorization: Bearer {access_token}
```

### 搜索联系人

```bash
POST https://api.hubapi.com/crm/v3/objects/contacts/search

{
  "filterGroups": [{
    "filters": [{
      "propertyName": "email",
      "operator": "EQ",
      "value": "user@example.com"
    }]
  }]
}
```

### 创建联系人

```bash
POST https://api.hubapi.com/crm/v3/objects/contacts

{
  "properties": {
    "email": "user@example.com",
    "firstname": "John",
    "lastname": "Doe",
    "company": "Example Inc"
  }
}
```

### 更新联系人

```bash
PATCH https://api.hubapi.com/crm/v3/objects/contacts/{contact_id}

{
  "properties": {
    "lifecyclestage": "customer"
  }
}
```

### 获取交易

```bash
GET https://api.hubapi.com/crm/v3/objects/deals?limit=10&properties=dealname,amount,dealstage

Authorization: Bearer {access_token}
```

### 创建交易

```bash
POST https://api.hubapi.com/crm/v3/objects/deals

{
  "properties": {
    "dealname": "New Deal",
    "amount": "10000",
    "dealstage": "appointmentscheduled",
    "pipeline": "default"
  }
}
```

### 将联系人与交易关联

```bash
PUT https://api.hubapi.com/crm/v3/objects/deals/{deal_id}/associations/contacts/{contact_id}/deal_to_contact
```

### 获取表单提交

```bash
GET https://api.hubapi.com/form-integrations/v1/submissions/forms/{form_guid}

Authorization: Bearer {access_token}
```

### 获取营销邮件

```bash
GET https://api.hubapi.com/marketing/v3/emails?limit=10

Authorization: Bearer {access_token}
```

## CLI 命令

```bash
# 安装
npm install -g @hubspot/cli

# 初始化项目
hs init

# 上传文件
hs upload src dest

# 监视更改
hs watch src dest

# 列出门户
hs accounts list
```

## 关键对象

- **Contacts** - CRM 中的人员
- **Companies** - 组织
- **Deals** - 销售机会
- **Tickets** - 支持工单
- **Products** - 待售商品
- **Line Items** - 交易行项目

## 常用属性

### 联系人属性
- `email` - 电子邮件地址
- `firstname`, `lastname` - 姓名
- `lifecyclestage` - 漏斗阶段
- `hs_lead_status` - 潜在客户状态

### 交易属性
- `dealname` - 交易名称
- `amount` - 交易价值
- `dealstage` - 管道阶段
- `closedate` - 预期关闭日期

## 使用时机

- 管理联系人和潜在客户
- 跟踪销售交易
- 营销自动化
- 表单提交
- 电子邮件活动
- 客户服务工单

## 速率限制

- 每 10 秒 100 次请求
- 企业计划有更高限制

## 相关技能

- email-sequence
- analytics-tracking
- referral-program
