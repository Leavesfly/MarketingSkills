# AirOps

AI 内容平台，用于创建能在 AI 搜索中胜出的内容。构建和执行 AI 工作流（flows），用于 SEO 内容生成、数据丰富和自动化。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Flows、Workflows、Runs |
| MCP | - | 不可用 |
| CLI | ✓ | [airops.js](../clis/airops.js) |
| SDK | - | 仅 REST API |

## 认证

- **类型**: API Key + Workspace ID
- **请求头**: `Authorization: Bearer {api_key}`
- **环境变量**: `AIROPS_API_KEY`、`AIROPS_WORKSPACE_ID`
- **获取密钥**: 在 https://app.airops.com 的设置 > API Keys 中获取

## 常用 Agent 操作

### 列出 Flows

```bash
GET https://api.airops.com/public_api/v1/workspaces/{workspace_id}/flows
```

### 获取 Flow 详情

```bash
GET https://api.airops.com/public_api/v1/workspaces/{workspace_id}/flows/{flow_id}
```

### 执行 Flow

```bash
POST https://api.airops.com/public_api/v1/workspaces/{workspace_id}/flows/{flow_id}/execute

{
  "inputs": {
    "keyword": "best project management tools",
    "target_audience": "startup founders"
  }
}
```

### 列出 Flow 的运行记录

```bash
GET https://api.airops.com/public_api/v1/workspaces/{workspace_id}/flows/{flow_id}/runs
```

### 获取运行状态

```bash
GET https://api.airops.com/public_api/v1/workspaces/{workspace_id}/runs/{run_id}
```

### 列出 Workflows

```bash
GET https://api.airops.com/public_api/v1/workspaces/{workspace_id}/workflows
```

### 执行 Workflow

```bash
POST https://api.airops.com/public_api/v1/workspaces/{workspace_id}/workflows/{workflow_id}/execute

{
  "inputs": {
    "topic": "email marketing best practices",
    "content_type": "blog_post"
  }
}
```

## 关键指标

### Flow 数据
- `id` - Flow 标识符
- `name` - Flow 名称
- `description` - Flow 描述
- `status` - 激活/停用状态
- `created_at` - 创建时间戳
- `updated_at` - 最后修改时间戳

### Run 数据
- `id` - Run 标识符
- `flow_id` - 父 Flow ID
- `status` - pending、running、completed、failed
- `inputs` - 使用的输入参数
- `outputs` - 生成的结果
- `started_at` - 运行开始时间
- `completed_at` - 运行完成时间

## 参数

### Flow 执行
- `inputs` - JSON 对象，键值对匹配 Flow 预期的输入
- 输入键因 Flow 而异（例如 `keyword`、`topic`、`url`、`target_audience`）

### Workflow 执行
- `inputs` - JSON 对象，键值对匹配 Workflow 预期的输入

## 适用场景

- 大规模批量生成 SEO 内容
- 使用 AI 工作流创建 SEO 优化文章
- 营销列表的数据丰富管道
- 关键词研究自动化
- 内容优化和重写
- 程序化 SEO 页面生成
- AI 驱动的内容简报和大纲

## 速率限制

- 速率限制根据套餐而异
- 并发执行限制取决于工作区层级
- 查看 AirOps 仪表板了解当前使用情况和限制

## 相关技能

- ai-seo
- content-strategy
- programmatic-seo
- copywriting
