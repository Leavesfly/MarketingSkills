# Coupler.io

数据集成平台,将营销、销售、分析和电子商务数据源连接到电子表格、BI 工具和数据仓库等目的地,支持自动化调度。

## 能力

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Importers、Runs、Sources、Destinations |
| MCP | ✓ | [Claude 连接器](https://claude.com/connectors/coupler-io) |
| CLI | ✓ | [coupler.js](../clis/coupler.js) |
| SDK | - | 仅 REST API |

## 认证

- **类型**: API Key
- **请求头**: `Authorization: Bearer {api_key}`
- **获取密钥**: Settings > API,访问 https://app.coupler.io

## 常见 Agent 操作

### 列出 Importers

```bash
GET https://api.coupler.io/v1/importers
```

### 获取 Importer 详情

```bash
GET https://api.coupler.io/v1/importers/{id}
```

### 触发 Importer 运行

```bash
POST https://api.coupler.io/v1/importers/{id}/run
```

### 创建 Importer

```bash
POST https://api.coupler.io/v1/importers

{
  "source_type": "google_analytics",
  "destination_type": "google_sheets",
  "name": "GA4 to Sheets Daily"
}
```

### 删除 Importer

```bash
DELETE https://api.coupler.io/v1/importers/{id}
```

### 列出 Importer 的运行记录

```bash
GET https://api.coupler.io/v1/importers/{id}/runs
```

### 获取运行详情

```bash
GET https://api.coupler.io/v1/runs/{id}
```

### 列出可用 Sources

```bash
GET https://api.coupler.io/v1/sources
```

### 列出可用 Destinations

```bash
GET https://api.coupler.io/v1/destinations
```

## 关键指标

### Importer 数据
- `id` - Importer ID
- `name` - Importer 名称
- `source_type` - 源连接器类型
- `destination_type` - 目标连接器类型
- `schedule` - 自动化调度
- `status` - 当前状态
- `last_run_at` - 最后运行时间戳

### Run 数据
- `id` - Run ID
- `importer_id` - 父级 importer
- `status` - 运行状态(pending、running、completed、failed)
- `started_at` - 开始时间戳
- `finished_at` - 结束时间戳
- `rows_imported` - 处理的行数
- `error` - 失败时的错误消息

## 参数

### Importer 创建
- `source_type` - 源连接器(例如:google_analytics、google_ads、facebook_ads、hubspot、shopify、stripe、airtable)
- `destination_type` - 目标连接器(例如:google_sheets、bigquery、snowflake、postgresql)
- `name` - Importer 名称
- `schedule` - 自动化调度(例如:hourly、daily、weekly)

### 支持的 Sources
- **分析**: Google Analytics、Adobe Analytics
- **广告**: Google Ads、Facebook Ads、LinkedIn Ads、TikTok Ads
- **CRM**: HubSpot、Salesforce、Pipedrive
- **电子商务**: Shopify、Stripe、WooCommerce
- **其他**: Airtable、Google Sheets、BigQuery、MySQL、PostgreSQL

### 支持的 Destinations
- **电子表格**: Google Sheets、Excel Online
- **BI 工具**: Looker Studio、Power BI、Tableau
- **数据仓库**: BigQuery、Snowflake、Redshift
- **数据库**: PostgreSQL、MySQL

## 何时使用

- 自动化从广告和分析平台到目的地的营销数据管道
- 将多渠道广告系列数据整合到单个目的地
- 安排从 CRM 到电子表格或 BI 工具的定期数据同步
- 使用来自多个来源的新鲜数据构建营销仪表板
- 导出电子商务数据用于报告和分析
- 无需编写自定义 ETL 代码即可连接数据源

## 速率限制

- 速率限制因计划而异
- 标准: Professional 及更高计划提供 API 访问
- Importer 运行频率取决于计划层级

## 相关技能

- analytics-tracking
- paid-ads
- revops
