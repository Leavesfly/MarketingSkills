# Firehose

实时网页数据流 API，监控网页并通过服务器发送事件（SSE）即时交付匹配内容。专为竞争情报、品牌监控和新闻追踪而构建，无需轮询。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | RESTful 端点用于管理规则 + SSE 用于流式传输 |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | - | 提供原生 AI 智能体技能 |

## 身份验证

- **类型**：API Key
- **当前状态**：免费测试版 — 无需信用卡
- **获取访问权限**：在 firehose.com 注册

## 核心概念

**规则** — 定义要匹配内容的过滤器。使用 Lucene 查询语法。

**流** — 服务器发送事件（SSE）连接，在内容发布到网络时实时交付匹配内容。

无需按计划轮询端点，只需定义一次规则，即可在匹配发生时接收持续的匹配流。

## 查询语法（Lucene）

```
# 精确短语
"your brand name"

# 字段特定查询
title:tesla
domain:reuters.com
domain:techcrunch.com

# 布尔运算符
"Series A" AND (SaaS OR software)
competitor OR "competitor name" NOT "your company"

# 通配符
market* AND funding

# 语言过滤
language:en

# 日期范围
publish_time:[2026-01-01 TO 2026-03-18]

# ML 分类类别
category:finance
category:technology
```

## 常见智能体操作

### 创建监控规则

```bash
POST https://api.firehose.com/rules

{
  "query": "\"your brand name\" OR \"your product name\"",
  "label": "brand-mentions"
}
```

### 列出活跃规则

```bash
GET https://api.firehose.com/rules
```

### 删除规则

```bash
DELETE https://api.firehose.com/rules/{rule_id}
```

### 连接到流

```bash
GET https://api.firehose.com/stream
Authorization: Bearer {api_key}

# 返回服务器发送事件：
# data: {"url": "...", "title": "...", "publish_time": "...", "matched_rule": "..."}
```

### 示例：Node.js 流消费者

```javascript
import EventSource from 'eventsource';

const stream = new EventSource('https://api.firehose.com/stream', {
  headers: { Authorization: `Bearer ${process.env.FIREHOSE_API_KEY}` }
});

stream.onmessage = (event) => {
  const item = JSON.parse(event.data);
  console.log(`[${item.matched_rule}] ${item.title} — ${item.url}`);
};
```

## 营销用例

### 竞争情报
实时监控竞争对手的新闻报道、产品发布和融资新闻。

```
query: "CompetitorName" AND (launch OR funding OR "product update" OR partnership)
```

### 品牌监控
跟踪您的品牌在新闻和网络内容中的提及情况。

```
query: "YourBrand" OR "YourProductName" NOT site:yourdomain.com
```

### 类别/市场新闻
无需手动检查来源即可了解市场动态。

```
query: category:technology AND ("no-code" OR "low-code") AND funding
domain:techcrunch.com OR domain:venturebeat.com
```

### 潜在客户触发监控
跟踪表明潜在客户准备购买的信号（招聘、融资、工具提及）。

```
query: ("hiring" OR "we're growing") AND "RevOps" AND (HubSpot OR Salesforce)
```

### PR 和链接建设
当出版物报道您所在领域的主题时收到提醒，以便及时进行外展。

```
query: "best [category] tools" OR "top [category] software" AND publish_time:[now-7d TO now]
```

## 何时使用

- 实时竞争情报（比 Google Alerts 更快）
- 跨新闻和网络的 brand mention 监控
- 销售潜在客户的 market signal 跟踪
- 自动化内容策划管道
- 基于触发器的工作流（新提及 → Slack 警报、CRM 更新等）

## 相关技能

- competitor-alternatives
- customer-research
- content-strategy
- cold-email
- marketing-ideas
