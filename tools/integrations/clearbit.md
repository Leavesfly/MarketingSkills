# Clearbit (HubSpot Breeze Intelligence)

公司和人员数据丰富 API,通过100+人口统计和技术属性转换潜在客户。

## 能力

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | 人员、公司、组合丰富、Reveal、名称到域名、Prospector |
| MCP | - | 不可用 |
| CLI | ✓ | [clearbit.js](../clis/clearbit.js) |
| SDK | ✓ | Node、Ruby、Python、PHP |

## 认证

- **类型**: Bearer Token(或使用 API key 作为用户名的 Basic Auth)
- **请求头**: `Authorization: Bearer {api_key}`
- **获取密钥**: https://dashboard.clearbit.com/api

## 常见 Agent 操作

### 人员丰富(通过电子邮件)

```bash
GET https://person.clearbit.com/v2/people/find?email=alex@clearbit.com
```

返回100+属性:姓名、职位、公司、位置、社交媒体资料、就业历史。

### 公司丰富(通过域名)

```bash
GET https://company.clearbit.com/v2/companies/find?domain=clearbit.com
```

返回人口统计数据:行业、规模、收入、技术栈、位置、融资情况。

### 组合丰富(人员 + 公司)

```bash
GET https://person.clearbit.com/v2/combined/find?email=alex@clearbit.com
```

在单个请求中返回人员和公司数据。

### Reveal(IP 到公司)

```bash
GET https://reveal.clearbit.com/v1/companies/find?ip=104.132.0.0
```

通过 IP 地址识别网站访客背后的公司。

### 名称到域名

```bash
GET https://company.clearbit.com/v1/domains/find?name=Clearbit
```

将公司名称转换为其域名。

### Prospector(查找员工)

```bash
GET https://prospector.clearbit.com/v1/people/search?domain=clearbit.com&role=sales&seniority=executive
```

按角色、资历、职位筛选查找公司员工。

## API 模式

Clearbit 为每个 API 使用不同的子域名:
- `person.clearbit.com` - 人员数据
- `company.clearbit.com` - 公司数据、名称到域名
- `person-stream.clearbit.com` - 流式人员查找(阻塞,最长60秒)
- `company-stream.clearbit.com` - 流式公司查找(阻塞,最长60秒)
- `reveal.clearbit.com` - IP 到公司
- `prospector.clearbit.com` - 员工搜索

标准端点在数据处理时返回 `202 Accepted`(使用 webhook)。流式端点会阻塞直到数据就绪。

## 关键指标

### 人员属性
- `name.fullName` - 全名
- `title` - 职位头衔
- `role` - 工作角色(sales、engineering 等)
- `seniority` - 资历级别
- `employment.name` - 公司名称
- `linkedin.handle` - LinkedIn 个人资料

### 公司属性
- `name` - 公司名称
- `domain` - 网站域名
- `category.industry` - 行业
- `metrics.employees` - 员工数量
- `metrics.estimatedAnnualRevenue` - 收入范围
- `tech` - 技术栈数组
- `metrics.raised` - 总融资额

## 参数

### 人员丰富
- `email` (必需) - 要查找的电子邮件地址
- `webhook_url` - 异步结果的 URL
- `subscribe` - 订阅未来更改

### 公司丰富
- `domain` (必需) - 要查找的公司域名
- `webhook_url` - 异步结果的 URL

### Prospector
- `domain` (必需) - 公司域名
- `role` - 工作角色过滤(sales、engineering、marketing 等)
- `seniority` - 资历过滤(executive、director、manager 等)
- `title` - 精确职位过滤
- `page` - 页码(默认: 1)
- `page_size` - 每页结果数(默认: 5,最大: 20)

## 何时使用

- 基于人口统计数据对潜在客户进行评分和资格认定
- 用公司和人员数据丰富 CRM 联系人
- 使用 Reveal 去匿名化网站访客
- 使用 Prospector 构建潜在客户列表
- 基于公司属性个性化营销
- 基于公司规模、行业或技术栈路由潜在客户

## 速率限制

- 丰富: 600 请求/分钟
- Prospector: 100 请求/分钟
- Reveal: 600 请求/分钟
- 响应包含 `X-RateLimit-Limit` 和 `X-RateLimit-Remaining` 请求头

## 相关技能

- lead-scoring
- personalization
- abm-strategy
- lead-enrichment
- competitor-alternatives
