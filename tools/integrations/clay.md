# Clay

数据丰富和外联自动化平台,用于通过75+数据提供商的水流式(enrichment)丰富功能构建潜在客户列表。

## 能力

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Tables、人员丰富、公司丰富 |
| MCP | ✓ | [Claude 连接器](https://claude.com/connectors/clay) |
| CLI | ✓ | [clay.js](../clis/clay.js) |
| SDK | - | 仅 REST API |

## 认证

- **类型**: API Key (Bearer token)
- **请求头**: `Authorization: Bearer {api_key}`
- **获取密钥**: Settings > API,访问 https://app.clay.com

## 常见 Agent 操作

### 列出表格

```bash
GET https://api.clay.com/v3/tables

Authorization: Bearer {api_key}
```

### 获取表格详情

```bash
GET https://api.clay.com/v3/tables/{table_id}

Authorization: Bearer {api_key}
```

### 获取表格行

```bash
GET https://api.clay.com/v3/tables/{table_id}/rows?page=1&per_page=25

Authorization: Bearer {api_key}
```

### 向表格添加行

```bash
POST https://api.clay.com/v3/tables/{table_id}/rows

{
  "first_name": "Jane",
  "last_name": "Doe",
  "company": "Acme Inc",
  "email": "jane@acme.com"
}
```

### 人员丰富

```bash
POST https://api.clay.com/v3/people/enrich

{
  "email": "jane@acme.com"
}
```

### 公司丰富

```bash
POST https://api.clay.com/v3/companies/enrich

{
  "domain": "acme.com"
}
```

## 关键指标

### 人员数据
- `first_name`, `last_name` - 姓名
- `email` - 电子邮件地址
- `title` - 职位头衔
- `linkedin_url` - LinkedIn 个人资料
- `company` - 公司名称
- `location` - 位置
- `seniority` - 资历级别

### 公司数据
- `name` - 公司名称
- `domain` - 网站域名
- `industry` - 行业
- `employee_count` - 员工数量
- `revenue` - 预估收入
- `location` - 总部位置
- `technologies` - 技术栈
- `description` - 公司描述

### 表格数据
- `id` - 表格 ID
- `name` - 表格名称
- `row_count` - 行数
- `columns` - 列定义
- `created_at` - 创建时间戳
- `updated_at` - 最后更新时间戳

## 参数

### 表格
- `page` - 页码(默认: 1)
- `per_page` - 每页结果数(默认: 25)

### 人员丰富
- `email` - 电子邮件地址
- `linkedin_url` - LinkedIn 个人资料 URL
- `first_name` + `last_name` - 基于姓名的查找

### 公司丰富
- `domain` - 公司域名(例如:"acme.com")

### 添加行
- 字段是动态的,与表格的列定义匹配
- 以键值对形式传递数据,匹配列名

## 何时使用

- 通过跨多个提供商的水流式丰富功能构建丰富的潜在客户列表
- 从75+来源用人员和公司数据丰富潜在客户
- 使用丰富数据自动化外联工作流
- 查找已验证的联系信息(电子邮件、电话号码、社交媒体资料)
- 公司研究和人口统计分析
- 通过 webhook 触发丰富工作流
- 将丰富数据同步回 CRM 或外联工具

## 速率限制

- 速率限制因计划而异
- 标准: 100 请求/分钟
- 企业计划有更高的限制
- 每次查找消耗的丰富积分因数据提供商而异
- Webhook 端点持续接受数据

## 相关技能

- cold-email
- revops
- sales-enablement
- competitor-alternatives
