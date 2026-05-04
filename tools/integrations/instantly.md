# Instantly.ai

冷邮件平台，内置邮箱预热和大规模营销活动管理功能。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API，支持营销活动、潜在客户、账户、分析 |
| MCP | - | 不可用 |
| CLI | [✓](../clis/instantly.js) | 零依赖 Node.js CLI |
| SDK | - | 仅 API |

## 认证

- **类型**: API Key（查询参数）
- **参数**: `api_key={key}`
- **环境变量**: `INSTANTLY_API_KEY`
- **获取密钥**: [Instantly 设置 > 集成 > API](https://app.instantly.ai/app/settings/integrations)

## 常见 Agent 操作

### 管理营销活动

```bash
# 列出营销活动
node tools/clis/instantly.js campaigns list --limit 20

# 获取营销活动详情
node tools/clis/instantly.js campaigns get --id cam_abc123

# 检查营销活动状态
node tools/clis/instantly.js campaigns status --id cam_abc123

# 启动营销活动
node tools/clis/instantly.js campaigns launch --id cam_abc123

# 暂停营销活动
node tools/clis/instantly.js campaigns pause --id cam_abc123
```

### 管理潜在客户

```bash
# 列出营销活动中的潜在客户
node tools/clis/instantly.js leads list --campaign-id cam_abc123 --limit 50

# 添加潜在客户
node tools/clis/instantly.js leads add --campaign-id cam_abc123 --email john@example.com --first-name John --last-name Doe --company "Example Inc"

# 删除潜在客户
node tools/clis/instantly.js leads delete --campaign-id cam_abc123 --email john@example.com

# 检查潜在客户状态
node tools/clis/instantly.js leads status --campaign-id cam_abc123 --email john@example.com
```

### 管理邮箱账户

```bash
# 列出已连接的账户
node tools/clis/instantly.js accounts list --limit 20

# 检查账户状态
node tools/clis/instantly.js accounts status --account-id me@example.com

# 检查预热状态
node tools/clis/instantly.js accounts warmup-status --account-id me@example.com
```

### 查看分析数据

```bash
# 营销活动分析
node tools/clis/instantly.js analytics campaign --campaign-id cam_abc123 --start 2024-01-01 --end 2024-01-31

# 分步分析
node tools/clis/instantly.js analytics steps --campaign-id cam_abc123

# 账户级别分析
node tools/clis/instantly.js analytics account --start 2024-01-01 --end 2024-01-31
```

### 管理黑名单

```bash
# 列出已屏蔽的邮箱/域名
node tools/clis/instantly.js blocklist list

# 添加到黑名单
node tools/clis/instantly.js blocklist add --entries "competitor.com,spam@example.com"
```

## 速率限制

- API 速率限制因套餐而异
- 建议：保持在每秒 10 次请求以下

## 使用场景

- **大规模链接建设**：运行大批量外展营销活动，内置预热功能
- **营销活动管理**：启动、暂停和监控冷邮件营销活动
- **账户健康**：监控邮箱账户预热和送达率
- **数据分析**：跟踪打开率、回复率和营销活动表现
