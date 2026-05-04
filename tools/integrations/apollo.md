# Apollo.io

B2B 潜在客户挖掘和数据丰富平台，拥有超过 2.1 亿联系人和 3500 万家公司数据，用于销售情报。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | People Search、Company Search、Enrichment、Sequences |
| MCP | - | 不可用 |
| CLI | ✓ | [apollo.js](../clis/apollo.js) |
| SDK | - | 仅 REST API |

## 认证

- **类型**: API Key
- **请求头**: `x-api-key: {api_key}` 或 `Authorization: Bearer {token}`
- **获取密钥**: 在 https://app.apollo.io 的设置 > Integrations > API 中获取

## 常用 Agent 操作

### 人员搜索

```bash
POST https://api.apollo.io/api/v1/mixed_people/api_search

{
  "person_titles": ["Sales Manager"],
  "person_locations": ["United States"],
  "organization_num_employees_ranges": ["1,100"],
  "page": 1
}
```

### 人员信息丰富化

```bash
POST https://api.apollo.io/api/v1/people/match

{
  "first_name": "Tim",
  "last_name": "Zheng",
  "domain": "apollo.io"
}
```

### 批量人员信息丰富化

```bash
POST https://api.apollo.io/api/v1/people/bulk_match

{
  "details": [
    { "email": "tim@apollo.io" },
    { "first_name": "Jane", "last_name": "Doe", "domain": "example.com" }
  ]
}
```

### 公司搜索

```bash
POST https://api.apollo.io/api/v1/mixed_companies/search

{
  "organization_locations": ["United States"],
  "organization_num_employees_ranges": ["1,100"],
  "page": 1
}
```

### 公司信息丰富化

```bash
POST https://api.apollo.io/api/v1/organizations/enrich

{
  "domain": "apollo.io"
}
```

## 关键指标

### 人员数据
- `first_name`、`last_name` - 姓名
- `title` - 职位头衔
- `email` - 已验证的邮箱
- `linkedin_url` - LinkedIn 个人资料链接
- `organization` - 公司详情
- `seniority` - 资历级别
- `departments` - 部门列表

### 公司数据
- `name` - 公司名称
- `website_url` - 网站
- `estimated_num_employees` - 员工数量
- `industry` - 行业
- `annual_revenue` - 年收入
- `technologies` - 技术栈
- `funding_total` - 总融资额

## 参数

### 人员搜索
- `person_titles` - 职位头衔数组
- `person_locations` - 地点数组
- `person_seniorities` - 资历级别数组：owner、founder、c_suite、partner、vp、head、director、manager、senior、entry
- `organization_num_employees_ranges` - 员工数量范围数组（例如 "1,100"）
- `organization_ids` - 按 Apollo 组织 ID 筛选
- `page` - 页码（默认：1）
- `per_page` - 每页结果数（默认：25，最大：100）

### 人员信息丰富化
- `email` - 邮箱地址
- `first_name` + `last_name` + `domain` - 替代查找方式
- `linkedin_url` - LinkedIn URL
- `reveal_personal_emails` - 包含个人邮箱
- `reveal_phone_number` - 包含电话号码

### 公司搜索
- `organization_locations` - 地点数组
- `organization_num_employees_ranges` - 员工数量范围
- `organization_ids` - 特定组织 ID
- `page` - 页码

## 适用场景

- 按角色、资历和公司规模构建目标潜在客户列表
- 使用已验证的联系信息丰富潜在客户
- 在目标账户中寻找决策者
- 公司研究和人口统计分析
- ABM 活动定位
- 销售情报和外部潜在客户挖掘

## 速率限制

- 速率限制根据套餐而异
- 标准版：大多数端点每分钟 100 个请求
- 批量丰富化：每个请求最多 10 人
- 搜索：最多 50,000 条记录（每页 100 条，共 500 页）

## 相关技能

- abm-strategy
- lead-enrichment
- lead-scoring
- cold-email
- competitor-alternatives
