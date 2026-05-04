# Hunter.io

用于外展和链接建设的电子邮件查找和验证平台。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API，支持域名搜索、邮箱查找、验证 |
| MCP | - | 不可用 |
| CLI | [✓](../clis/hunter.js) | 零依赖 Node.js CLI |
| SDK | - | 仅 API |

## 认证

- **类型**: API Key（查询参数）
- **参数**: `api_key={key}`
- **环境变量**: `HUNTER_API_KEY`
- **获取密钥**: [Hunter 控制台 > API](https://hunter.io/api-keys)

## 常见 Agent 操作

### 查找域名的邮箱

```bash
node tools/clis/hunter.js domain search --domain example.com --limit 10
```

### 查找特定人员的邮箱

```bash
node tools/clis/hunter.js email find --domain example.com --first-name John --last-name Doe
```

### 验证邮箱地址

```bash
node tools/clis/hunter.js email verify --email john@example.com
```

### 统计域名可用的邮箱数量

```bash
node tools/clis/hunter.js domain count --domain example.com
```

### 管理潜在客户

```bash
# 列出潜在客户
node tools/clis/hunter.js leads list --limit 20

# 创建潜在客户
node tools/clis/hunter.js leads create --email john@example.com --first-name John --last-name Doe --company "Example Inc"

# 删除潜在客户
node tools/clis/hunter.js leads delete --id 12345
```

### 管理营销活动

```bash
# 列出营销活动
node tools/clis/hunter.js campaigns list

# 获取营销活动详情
node tools/clis/hunter.js campaigns get --id 12345

# 启动/暂停营销活动
node tools/clis/hunter.js campaigns start --id 12345
node tools/clis/hunter.js campaigns pause --id 12345
```

### 检查账户使用情况

```bash
node tools/clis/hunter.js account info
```

## 速率限制

- 免费套餐：每月 25 次搜索，50 次验证
- 付费套餐随等级扩展
- API 速率限制：每秒 10 次请求

## 使用场景

- **链接建设**：在目标域名中查找联系人邮箱以进行外展
- **潜在客户开发**：从公司域名构建潜在客户列表
- **验证**：在发送营销活动前清理邮箱列表
