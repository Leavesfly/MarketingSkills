# Composio

通过单个 MCP 服务器为500+应用提供托管 OAuth 和预构建工具连接器。为缺乏原生 MCP 支持的营销工具提供 agent 原生的访问能力。

## 能力

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API 用于管理连接和触发动作 |
| MCP | ✓ | 单个 MCP 服务器暴露所有连接的工具 |
| CLI | ✓ | `npx composio` 用于管理应用、连接和动作 |
| SDK | ✓ | TypeScript 和 Python SDK |

## 认证

- **类型**: OAuth 2.0(每个工具,由 Composio 管理)或 API Key
- **设置**: `npx @composio/mcp@latest setup` 安装,然后通过浏览器中的 Connect Link 对每个工具进行身份验证
- **API Key**(可选): `COMPOSIO_API_KEY` 环境变量用于高级/团队使用

Composio 处理所有连接工具的 OAuth token 管理、刷新和存储。各个工具的身份验证类型列在下方的营销工具表中。

## 何时使用 Composio vs. 原生工具

Composio 是一种**替代集成方法**,而非替代品。使用此决策指南:

| 场景 | 使用 |
|----------|-----|
| 工具有原生 MCP 服务器(GA4、Stripe、Mailchimp) | 原生 MCP 服务器 |
| 工具有 CLI 但无 MCP(Meta Ads、LinkedIn Ads、HubSpot) | Composio 用于 MCP 访问 |
| OAuth 繁重的工具且无 CLI(Google Sheets、Slack、Notion) | Composio |
| 需要深度、定制化集成 | 原生 API + CLI |
| 需要在多个工具间快速读/写访问 | Composio |
| Composio 未覆盖的工具 | 原生 API 指南 |

## 设置

### 1. 安装 MCP 服务器

```bash
npx @composio/mcp@latest setup
```

这会将 Composio MCP 服务器添加到你的 Claude Code 配置中。

### 2. 验证安装

在 Claude Code 中,运行 `/mcp` 确认 `composio` 出现在你的 MCP 服务器列表中。

### 3. 对工具进行身份验证

当你首次使用 Composio 支持的工具时,你将收到一个 Connect Link。在浏览器中打开它以完成 OAuth。连接会在会话之间保持。

```
# 示例:连接 HubSpot
> "Pull my top 10 HubSpot contacts"
# Agent 将提示:"Please authenticate HubSpot: [Connect Link]"
# 点击链接 → 授权 → 完成
```

### 4. API key(可选)

对于高级用法或团队设置,设置你的 Composio API key:

```bash
export COMPOSIO_API_KEY=your_key_here
```

## 通过 Composio 可用的营销工具

### 新的 MCP 覆盖

这些工具在此仓库中有 API 指南,但**没有原生 MCP 服务器**。Composio 添加了 MCP 访问:

| 工具 | Composio Toolkit | 认证类型 | 覆盖深度 |
|------|-----------------|-----------|----------------|
| HubSpot | `HUBSPOT` | OAuth 2.0 | 深(联系人、交易、公司、列表、电子邮件) |
| Salesforce | `SALESFORCE` | OAuth 2.0 | 深(SOQL、对象、潜在客户、机会) |
| Meta Ads | `FACEBOOKADS` | OAuth 2.0 | 中(广告系列、广告组、洞察) |
| LinkedIn Ads | `LINKEDIN` | OAuth 2.0 | 中(广告系列、分析、公司页面) |
| Google Sheets | `GOOGLESHEETS` | OAuth 2.0 | 深(读取、写入、创建、格式化) |
| Slack | `SLACK` | OAuth 2.0 | 深(消息、频道、文件) |
| Notion | `NOTION` | OAuth 2.0 | 深(页面、数据库、块) |
| Airtable | `AIRTABLE` | OAuth 2.0 | 深(记录、表、视图) |
| ActiveCampaign | `ACTIVECAMPAIGN` | API Key | 中(联系人、列表、自动化) |
| Klaviyo | `KLAVIYO` | API Key | 中(个人资料、列表、活动) |
| Shopify | `SHOPIFY` | OAuth 2.0 | 深(产品、订单、客户) |
| Gmail | `GMAIL` | OAuth 2.0 | 深(读取、发送、标签、搜索) |

### 现有工具的替代方案

这些工具在此仓库中**已有原生 MCP 或 CLI**。Composio 提供替代路径:

| 工具 | 原生集成 | Composio Toolkit | 何时使用 Composio |
|------|-------------------|-----------------|---------------------|
| Mailchimp | MCP ✓, CLI ✓ | `MAILCHIMP` | 如果原生 MCP 设置失败 |
| Google Ads | MCP ✓, CLI ✓ | `GOOGLEADS` | 如果通过 Composio OAuth 更简单 |
| Stripe | MCP ✓, CLI ✓ | `STRIPE` | 优先使用原生(更深覆盖) |
| GA4 | MCP ✓, CLI ✓ | `GOOGLEANALYTICS` | 优先使用原生(更深覆盖) |

## 常见 Agent 操作

### 列出可用工具

```bash
# 通过 Composio CLI
npx composio apps list
```

### 检查连接状态

```bash
npx composio connections list
```

### 以编程方式触发动作

```bash
POST https://backend.composio.dev/api/v1/actions/{action_id}/execute

{
  "connectedAccountId": "account_xxx",
  "input": {
    "query": "contact email = user@example.com"
  }
}
```

### 断开工具连接

```bash
npx composio connections remove {connection_id}
```

## 示例工作流

### 将 CRM 数据拉入电子表格

```
> "Get my top 20 HubSpot contacts by last activity and add them to a Google Sheet"
```
Agent 使用 Composio 的 `HUBSPOT` 获取联系人,并使用 `GOOGLESHEETS` 写入行。

### 跨平台广告报告

```
> "Compare my Meta Ads and LinkedIn Ads spend this month"
```
Agent 使用 `FACEBOOKADS` 和 `LINKEDIN` toolkit 拉取广告系列数据。

### 通知团队关于新潜在客户

```
> "Get my Salesforce leads from today and post a summary in Slack #sales"
```
Agent 使用 `SALESFORCE` 读取潜在客户,并使用 `SLACK` 发布消息。

## 限制

- **覆盖深度不同** — 某些 toolkit 公开数百个动作(HubSpot、Google Sheets),其他只有少数几个
- **无定制** — 你无法修改 Composio 的动作 schema 或添加自定义端点
- **供应商依赖** — 如果 Composio 的服务器宕机,所有连接的工具都不可用
- **速率限制适用** — Composio 在每个工具的原生限制之上实施自己的速率限制
- **OAuth tokens** — 由 Composio 管理;你无法控制 token 刷新或存储
- **动作命名** — Composio 动作名称可能与原生 API 术语不同

## 定价

| 计划 | 月费 | API 调用 | 说明 |
|------|--------------|-----------|-------|
| Free | $0 | 20,000 | 适合探索和个人使用 |
| Growth | $29 | 200,000 | 适合跨多个工具的常规使用 |
| Business | $229 | 2,000,000 | 适合团队和重度自动化 |

## 速率限制

- Free tier: 20,000 调用/月,10 req/sec
- Growth tier: 200,000 调用/月,50 req/sec
- Business tier: 2,000,000 调用/月,100 req/sec

## 另请参阅

- [快速入门指南](../composio/README.md) — 5分钟内安装、连接和使用
- [营销工具映射](../composio/marketing-tools.md) — 详细的 toolkit 到类别参考

## 相关技能

- analytics-tracking(通过 Composio 连接器的跨平台数据)
- email-sequence(ActiveCampaign、Klaviyo 访问)
- paid-ads(Meta Ads、LinkedIn Ads MCP 访问)
- referral-program(Shopify 集成)
