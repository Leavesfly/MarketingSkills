# Contentful

企业级无头 CMS,支持多语言、双 API 架构和可组合内容。

## 能力

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Content Delivery API(读取)、Content Management API(写入) |
| MCP | - | 无官方 MCP 服务器 |
| CLI | ✓ | `contentful-cli` 用于 spaces、content types、migrations |
| SDK | ✓ | `contentful`(delivery)、`contentful-management`(management) |

## 认证

- **Delivery API (CDA)**: `Authorization: Bearer {delivery_token}`
  - 基础 URL: `https://cdn.contentful.com`
  - 只读,CDN 缓存
- **Preview API (CPA)**: `Authorization: Bearer {preview_token}`
  - 基础 URL: `https://preview.contentful.com`
  - 只读,返回草稿内容
- **Management API (CMA)**: `Authorization: Bearer {management_token}`
  - 基础 URL: `https://api.contentful.com`
  - 读/写,不缓存
- **Tokens**: 在 Settings → API keys(delivery)或 Settings → CMA tokens(management)中创建

## 常见 Agent 操作

### 获取条目(Delivery API)

```bash
GET https://cdn.contentful.com/spaces/{space_id}/environments/{environment}/entries?content_type=blogPost&limit=10

Authorization: Bearer {delivery_token}
```

### 获取单个条目

```bash
GET https://cdn.contentful.com/spaces/{space_id}/environments/{environment}/entries/{entry_id}

Authorization: Bearer {delivery_token}
```

### 搜索和过滤

```bash
# 按字段值
GET https://cdn.contentful.com/spaces/{space_id}/environments/{environment}/entries?content_type=blogPost&fields.slug=my-post

# 全文搜索
GET https://cdn.contentful.com/spaces/{space_id}/environments/{environment}/entries?query=marketing+strategy

# 按日期范围
GET https://cdn.contentful.com/spaces/{space_id}/environments/{environment}/entries?content_type=blogPost&fields.publishDate[gte]=2024-01-01
```

### 创建条目(Management API)

CMA 使用 PUT 和客户端生成的 `entry_id`。要自动生成,使用 POST 且路径中不包含 ID。

```bash
PUT https://api.contentful.com/spaces/{space_id}/environments/{environment}/entries/{entry_id}
Content-Type: application/vnd.contentful.management.v1+json
X-Contentful-Content-Type: blogPost
Authorization: Bearer {management_token}

{
  "fields": {
    "title": {"en-US": "New Post"},
    "slug": {"en-US": "new-post"},
    "body": {"en-US": "Post content here"}
  }
}
```

### 更新条目

```bash
PUT https://api.contentful.com/spaces/{space_id}/environments/{environment}/entries/{entry_id}
Content-Type: application/vnd.contentful.management.v1+json
X-Contentful-Version: {current_version}
Authorization: Bearer {management_token}

{
  "fields": {
    "title": {"en-US": "Updated Title"}
  }
}
```

### 发布条目

```bash
PUT https://api.contentful.com/spaces/{space_id}/environments/{environment}/entries/{entry_id}/published
X-Contentful-Version: {current_version}
Authorization: Bearer {management_token}
```

### 取消发布条目

```bash
DELETE https://api.contentful.com/spaces/{space_id}/environments/{environment}/entries/{entry_id}/published
X-Contentful-Version: {current_version}
Authorization: Bearer {management_token}
```

## CLI 命令

```bash
# 登录
contentful login

# 列出 spaces
contentful space list

# 导出 space 内容
contentful space export --space-id {space_id}

# 导入内容
contentful space import --space-id {space_id} --content-file export.json

# 创建 migration
contentful space migration --space-id {space_id} migration.js

# 列出 content types
contentful content-type list --space-id {space_id}
```

## 关键对象

- **Space** — 内容的顶层容器(每个项目一个)
- **Environment** — 隔离的内容分支(`master`、`staging` 等)
- **Content Type** — 带有字段和验证的模式定义
- **Entry** — 特定 content type 的内容项
- **Asset** — 媒体文件(图片、视频、文档)
- **Locale** — 语言/地区变体(例如:`en-US`、`de-DE`)

## 何时使用

- 多语言营销内容(全球网站)
- 具有审批工作流的企业内容运营
- 可组合内容架构
- 需要成熟供应商支持和 SLA 的团队
- 跨多个渠道的内容复用

## 速率限制

速率限制取决于计划。检查 `X-Contentful-RateLimit-Second-Limit` 响应头以获取你的实际限制。

- Delivery API (CDA): 因计划而异(通常高吞吐量)
- Preview API (CPA): 低于 CDA(因计划而异)
- Management API (CMA): 约 10 请求/秒(默认)
- 参见 [Contentful 技术限制](https://www.contentful.com/developers/docs/technical-limits/)获取当前值

## 相关技能

- content-strategy(CMS 选择、内容建模)
- programmatic-seo(CMS 作为生成页面的数据源)
- site-architecture(多语言 URL 结构)
