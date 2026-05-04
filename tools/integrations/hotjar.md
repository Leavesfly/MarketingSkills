# Hotjar

行为分析平台，提供热力图、会话录制和调查功能，用于理解用户体验。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Surveys、Responses、Sites、Heatmaps、Recordings |
| MCP | - | 不可用 |
| CLI | ✓ | [hotjar.js](../clis/hotjar.js) |
| SDK | ✓ | JavaScript 跟踪代码片段、Identify API、Events API |

## 身份验证

- **类型**：OAuth 2.0 Client Credentials
- **令牌端点**：`POST https://api.hotjar.io/v1/oauth/token`
- **请求头**：`Authorization: Bearer {access_token}`
- **获取凭据**：Hotjar Dashboard > Integrations > API
- **令牌有效期**：3600 秒（1 小时）

### 令牌请求

```bash
POST https://api.hotjar.io/v1/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id={client_id}&client_secret={client_secret}
```

### 令牌响应

```json
{
  "access_token": "<token>",
  "token_type": "Bearer",
  "expires_in": 3600
}
```

## 常见代理操作

### 列出站点

```bash
GET https://api.hotjar.io/v1/sites

Authorization: Bearer {access_token}
```

### 列出调查

```bash
GET https://api.hotjar.io/v1/sites/{site_id}/surveys

Authorization: Bearer {access_token}
```

### 获取调查回复

```bash
GET https://api.hotjar.io/v1/sites/{site_id}/surveys/{survey_id}/responses?limit=100

Authorization: Bearer {access_token}
```

支持使用 `cursor` 和 `limit` 参数进行基于游标的分页。

### 列出热力图

```bash
GET https://api.hotjar.io/v1/sites/{site_id}/heatmaps

Authorization: Bearer {access_token}
```

### 列出录制

```bash
GET https://api.hotjar.io/v1/sites/{site_id}/recordings

Authorization: Bearer {access_token}
```

### 列出表单

```bash
GET https://api.hotjar.io/v1/sites/{site_id}/forms

Authorization: Bearer {access_token}
```

## 关键指标

### 调查回复数据
- `response_id` - 唯一回复标识符
- `answers` - 问题/答案对数组
- `created_at` - 回复时间戳
- `device_type` - 桌面端、移动端、平板

### 热力图数据
- `url` - 页面 URL
- `click_count` - 跟踪的总点击次数
- `visitors` - 独立访客
- `created_at` - 热力图创建日期

### 录制数据
- `recording_id` - 唯一录制 ID
- `duration` - 会话时长
- `pages_visited` - 会话中的页面数
- `device` - 设备信息

## 参数

### 调查回复
- `limit` - 每页结果数（默认：100）
- `cursor` - 上一页响应中的分页游标
- `sort` - 排序顺序（默认：created_at desc）

### 录制
- `limit` - 每页结果数
- `cursor` - 分页游标
- `date_from` - 开始日期过滤器
- `date_to` - 结束日期过滤器

## 使用时机

- 分析着陆页上的用户行为模式
- 通过站内调查收集定性反馈
- 通过会话录制识别 UX 问题
- 通过热力图了解滚动深度和参与度
- 使用用户行为数据验证 CRO 假设
- 表单放弃分析

## 速率限制

- 每分钟 3000 次请求（每秒 50 次）
- 按源 IP 地址进行速率限制
- 大型结果集使用基于游标的分页

## 相关技能

- page-cro
- ab-test-setup
- analytics-tracking
- ux-audit
- landing-page
