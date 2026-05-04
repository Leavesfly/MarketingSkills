# Crossbeam

合作伙伴生态系统平台(现属于 Reveal),用于与合作伙伴共享账户数据以识别联合销售机会、重叠客户和合作伙伴来源的管道。

## 能力

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Partners、Populations、Overlaps、Reports、Threads |
| MCP | ✓ | [Claude 连接器](https://claude.com/connectors/crossbeam) |
| CLI | ✓ | [crossbeam.js](../clis/crossbeam.js) |
| SDK | - | 仅 REST API |

## 认证

- **类型**: API Key
- **请求头**: `Authorization: Bearer {api_key}`
- **获取密钥**: Settings > API,访问 https://app.crossbeam.com

## 常见 Agent 操作

### 列出 Partners

```bash
GET https://api.crossbeam.com/v1/partners
Authorization: Bearer {api_key}
```

### 获取 Partner 详情

```bash
GET https://api.crossbeam.com/v1/partners/{id}
Authorization: Bearer {api_key}
```

### 列出 Populations

```bash
GET https://api.crossbeam.com/v1/populations
Authorization: Bearer {api_key}
```

### 列出 Overlaps

```bash
GET https://api.crossbeam.com/v1/overlaps?partner_id={partner_id}&population_id={population_id}
Authorization: Bearer {api_key}
```

### 获取 Overlap 详情

```bash
GET https://api.crossbeam.com/v1/overlaps/{id}
Authorization: Bearer {api_key}
```

### 搜索 Accounts

```bash
GET https://api.crossbeam.com/v1/accounts/search?domain={domain}
Authorization: Bearer {api_key}
```

### 列出 Reports

```bash
GET https://api.crossbeam.com/v1/reports
Authorization: Bearer {api_key}
```

### 列出协作 Threads

```bash
GET https://api.crossbeam.com/v1/threads
Authorization: Bearer {api_key}
```

## 关键指标

### Partner 数据
- `id` - Partner ID
- `name` - 合作伙伴公司名称
- `status` - 合作关系状态(active、pending 等)
- `created_at` - 合作关系建立时间
- `populations_shared` - 共享的 populations 数量

### Population 数据
- `id` - Population ID
- `name` - Population 名称(例如:"Customers"、"Open Opportunities")
- `record_count` - Population 中的记录数
- `partner_visibility` - 合作伙伴可见的内容

### Overlap 数据
- `id` - Overlap ID
- `partner_id` - 涉及的合作伙伴
- `population_id` - 匹配的 population
- `account_name` - 重叠账户名称
- `overlap_type` - 重叠类型(customer、prospect 等)
- `match_confidence` - 匹配置信度评分

### Report 数据
- `id` - Report ID
- `name` - Report 名称
- `type` - Report 类型
- `created_at` - 创建日期
- `results` - Report 结果数据

## 参数

### Overlaps 列表
- `partner_id` - 按特定合作伙伴过滤
- `population_id` - 按特定 population 过滤

### Accounts 搜索
- `domain` - 要搜索的公司域名

## 何时使用

- 识别与渠道合作伙伴的联合销售机会
- 在合作伙伴生态系统中查找重叠的客户和潜在客户
- 通过匹配账户构建合作伙伴来源的管道
- 跟踪合作伙伴对交易的影响
- 为合作伙伴会议创建账户映射报告
- 基于重叠数据确定优先接触的合作伙伴

## 速率限制

- 速率限制因计划而异
- 标准: 100 请求/分钟
- 列表端点支持分页

## 相关技能

- revops
- sales-enablement
- referral-program
- competitor-alternatives
