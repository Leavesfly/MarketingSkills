# Composio 快速开始

通过一次集成即可获得对 500+ 营销工具的 MCP 访问能力。

## 先决条件

- Node.js 18+
- 已安装 Claude Code

## 安装

```bash
npx @composio/mcp@latest setup
```

在 Claude Code 中运行 `/mcp` 进行验证 —— `composio` 应出现在服务器列表中。

## 连接工具

当你第一次要求 agent 使用由 Composio 支持的工具时，它会提供一个 Connect Link。在浏览器中打开该链接，授权应用，即可完成连接。连接会在多次会话之间保持有效。

```
You: "Get my top HubSpot contacts"
Agent: "Please connect HubSpot first: https://app.composio.dev/connect/..."
# Click the link → authorize → return to Claude Code
Agent: "Here are your top contacts: ..."
```

## 使用示例

### 拉取 CRM 联系人

```
"Show me my 10 most recent HubSpot contacts with their deal stages"
```

### 获取广告表现

```
"What's my Meta Ads spend and ROAS for the last 7 days?"
```

### 写入电子表格

```
"Add a row to my 'Campaign Tracker' Google Sheet with today's LinkedIn Ads metrics"
```

### 跨工具工作流

```
"Find Salesforce leads from this week and post a summary in Slack #new-leads"
```

## 可用的营销工具

完整的 Composio 工具包与营销用例映射列表，请参见 [marketing-tools.md](marketing-tools.md)。

通过此集成新增 MCP 访问能力的关键工具（本仓库未提供原生 MCP 服务器）：
- **HubSpot** —— 联系人、交易、公司、列表
- **Salesforce** —— SOQL 查询、线索、商机
- **Meta Ads** —— 广告系列、广告组、洞察数据
- **LinkedIn Ads** —— 广告系列、分析数据
- **Google Sheets** —— 读取、写入、创建电子表格
- **Slack** —— 消息、频道
- **Notion** —— 页面、数据库
- **Klaviyo** —— 用户档案、列表、营销活动
- **ActiveCampaign** —— 联系人、自动化

## 故障排查

### "Tool not found" 错误

该工具可能尚未连接。可以让 agent 去连接，或运行：

```bash
npx composio apps list
```

### 认证过期

OAuth token 会过期。如果某个工具无法工作，请重新认证：

```bash
npx composio connections list    # Find the connection
npx composio connections remove {id}  # Remove it
# Then ask the agent to use the tool again to trigger re-auth
```

### 限流错误

Composio 有自己的速率限制（免费版：每月 20K 次调用，每秒 10 次请求）。如果触发限制：
- 降低请求频率
- 升级你的 Composio 套餐
- 大批量操作改用原生 CLI 工具

### MCP 服务器未出现

重新运行 setup 命令：

```bash
npx @composio/mcp@latest setup
```

然后重启 Claude Code。
