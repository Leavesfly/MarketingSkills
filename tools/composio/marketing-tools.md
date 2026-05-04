# Composio 营销工具

Composio 工具包与营销用例的详细映射。分类与 [REGISTRY.md](../REGISTRY.md) 保持一致。

## CRM

| Composio 工具包 | 认证方式 | 关键营销动作 | 覆盖深度 |
|-----------------|------|----------------------|-------|
| `HUBSPOT` | OAuth 2.0 | 获取/创建联系人、按阶段列出交易、获取公司信息、管理列表、按属性搜索联系人 | 深度 |
| `SALESFORCE` | OAuth 2.0 | 执行 SOQL 查询、获取/创建线索、列出商机、获取账户详情、更新记录 | 深度 |

## 邮件与短信

| Composio 工具包 | 认证方式 | 关键营销动作 | 覆盖深度 |
|-----------------|------|----------------------|-------|
| `ACTIVECAMPAIGN` | API Key | 获取联系人、列出自动化流程、将联系人加入列表、获取营销活动数据 | 中等 |
| `KLAVIYO` | API Key | 获取用户档案、列出分群、获取营销活动指标、加入列表 | 中等 |
| `MAILCHIMP` | OAuth 2.0 | 获取受众、列出营销活动、获取活动报告、添加订阅者 | 深度 |
| `GMAIL` | OAuth 2.0 | 发送邮件、搜索收件箱、读取邮件、管理标签 | 深度 |

## 广告投放

| Composio 工具包 | 认证方式 | 关键营销动作 | 覆盖深度 |
|-----------------|------|----------------------|-------|
| `FACEBOOKADS` | OAuth 2.0 | 获取广告系列洞察、列出广告组、获取广告表现、读取受众数据 | 中等 |
| `LINKEDIN` | OAuth 2.0 | 获取广告系列分析数据、列出广告系列、获取公司主页统计 | 中等 |
| `GOOGLEADS` | OAuth 2.0 | 获取广告系列表现、列出广告组、关键词数据 | 中等 |

## 办公与协作

| Composio 工具包 | 认证方式 | 关键营销动作 | 覆盖深度 |
|-----------------|------|----------------------|-------|
| `GOOGLESHEETS` | OAuth 2.0 | 读写单元格、创建表格、格式化区域、追加行 | 深度 |
| `SLACK` | OAuth 2.0 | 发送消息、读取频道、上传文件、搜索消息 | 深度 |
| `NOTION` | OAuth 2.0 | 读取/创建页面、查询数据库、更新块、搜索 | 深度 |
| `AIRTABLE` | OAuth 2.0 | 列出/创建/更新记录、查询视图、管理表格 | 深度 |

## 电商

| Composio 工具包 | 认证方式 | 关键营销动作 | 覆盖深度 |
|-----------------|------|----------------------|-------|
| `SHOPIFY` | OAuth 2.0 | 获取产品、列出订单、获取客户数据、库存水平 | 深度 |

## 分析

| Composio 工具包 | 认证方式 | 关键营销动作 | 覆盖深度 |
|-----------------|------|----------------------|-------|
| `GOOGLEANALYTICS` | OAuth 2.0 | 运行报表、获取实时数据、列出属性 | 中等 |

## 覆盖深度说明

- **深度** —— 20+ 个动作，覆盖大部分常见操作，适合日常使用
- **中等** —— 5-20 个动作，覆盖核心读操作和部分写操作
- **浅度** —— 少于 5 个动作，仅支持基础只读访问

## 覆盖范围 vs. 原生工具

下表展示 Composio 相较 MarketingSkills 注册表中已有工具在何处提供了增量价值：

| 工具 | 原生 MCP | 原生 CLI | Composio MCP | 建议 |
|------|:----------:|:----------:|:------------:|----------------|
| HubSpot | - | ✓ | ✓ | **使用 Composio** —— 新增 MCP 访问能力 |
| Salesforce | - | ✓ | ✓ | **使用 Composio** —— 新增 MCP 访问能力 |
| Meta Ads | - | ✓ | ✓ | **使用 Composio** —— 新增 MCP 访问能力 |
| LinkedIn Ads | - | ✓ | ✓ | **使用 Composio** —— 新增 MCP 访问能力 |
| Google Sheets | - | - | ✓ | **使用 Composio** —— 唯一 MCP 方案 |
| Slack | - | - | ✓ | **使用 Composio** —— 唯一 MCP 方案 |
| Notion | - | - | ✓ | **使用 Composio** —— 唯一 MCP 方案 |
| Airtable | - | - | ✓ | **使用 Composio** —— 唯一 MCP 方案 |
| ActiveCampaign | - | ✓ | ✓ | **使用 Composio** —— 新增 MCP 访问能力 |
| Klaviyo | - | ✓ | ✓ | **使用 Composio** —— 新增 MCP 访问能力 |
| Shopify | - | ✓ | ✓ | **使用 Composio** —— 新增 MCP 访问能力 |
| Gmail | - | - | ✓ | **使用 Composio** —— 唯一 MCP 方案 |
| GA4 | ✓ | ✓ | ✓ | **使用原生工具** —— 覆盖更深 |
| Stripe | ✓ | ✓ | ✓ | **使用原生工具** —— 覆盖更深 |
| Mailchimp | ✓ | ✓ | ✓ | **使用原生工具** —— 覆盖更深 |
| Google Ads | ✓ | ✓ | ✓ | **使用原生工具** —— 覆盖更深 |

## 工具包参考

每个 Composio 工具包名对应其在 Composio 平台中使用的 `TOOL_NAME` 标识符。搜索可用动作时，请使用这些精确名称：

```bash
# List all actions for a toolkit
npx composio actions list --app HUBSPOT

# Search for specific actions
npx composio actions list --app FACEBOOKADS --search "insights"
```

完整的集成指南（包括安装、定价与限制）请参见 [composio.md](../integrations/composio.md)。
