# Buffer

社交媒体调度、发布和分析平台，用于管理多个社交资料。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API v1，支持 profiles、updates、scheduling |
| MCP | - | 不可用 |
| CLI | ✓ | [buffer.js](../clis/buffer.js) |
| SDK | - | 无官方 SDK；旧版 API 仍受支持 |

## 认证

- **类型**: OAuth 2.0 Bearer Token
- **请求头**: `Authorization: Bearer {access_token}`
- **获取密钥**: 在 https://buffer.com/developers/apps 注册应用，然后完成 OAuth 流程
- **注意**: Buffer 不再接受新的开发者应用注册；现有应用继续有效。新的公共 API 正在开发中，详见 https://buffer.com/developer-api

## 常用 Agent 操作

### 获取用户信息

```bash
GET https://api.bufferapp.com/1/user.json

Authorization: Bearer {token}
```

### 列出已连接的资料

```bash
GET https://api.bufferapp.com/1/profiles.json

Authorization: Bearer {token}
```

### 获取资料发布计划

```bash
GET https://api.bufferapp.com/1/profiles/{profile_id}/schedules.json
```

### 创建定时帖子

```bash
POST https://api.bufferapp.com/1/updates/create.json
Content-Type: application/x-www-form-urlencoded

profile_ids[]={profile_id}&text=Your+post+content&scheduled_at=2026-03-01T10:00:00Z
```

### 获取资料的待发布更新

```bash
GET https://api.bufferapp.com/1/profiles/{profile_id}/updates/pending.json?count=25
```

### 获取资料的已发送更新

```bash
GET https://api.bufferapp.com/1/profiles/{profile_id}/updates/sent.json?count=25
```

### 立即发布待发布更新

```bash
POST https://api.bufferapp.com/1/updates/{update_id}/share.json
```

### 删除更新

```bash
POST https://api.bufferapp.com/1/updates/{update_id}/destroy.json
```

### 重新排序队列

```bash
POST https://api.bufferapp.com/1/profiles/{profile_id}/updates/reorder.json
Content-Type: application/x-www-form-urlencoded

order[]={update_id_1}&order[]={update_id_2}&order[]={update_id_3}
```

## API 模式

Buffer API v1 在所有端点上使用 `.json` 扩展名。POST 请求使用 `application/x-www-form-urlencoded` 内容类型。数组参数使用方括号表示法（例如 `profile_ids[]`）。

响应在变更操作中包含 `success` 布尔值。

## 关键指标

### 资料指标
- `followers` - 已连接资料的粉丝数
- `service` - 平台名称（twitter、facebook、instagram、linkedin 等）

### 更新指标（已发送更新）
- `statistics.reach` - 帖子触达人数
- `statistics.clicks` - 链接点击数
- `statistics.retweets` - 转发/分享数
- `statistics.favorites` - 点赞/收藏数
- `statistics.mentions` - 提及数

## 参数

### 更新创建参数
- `profile_ids[]` - 必需。要发布的资料 ID 数组
- `text` - 必需。帖子内容
- `scheduled_at` - ISO 8601 时间戳，用于调度
- `now` - 设置为 `true` 以立即发布
- `top` - 设置为 `true` 以添加到队列顶部
- `shorten` - 设置为 `true` 以自动缩短链接
- `media[photo]` - 照片附件 URL
- `media[thumbnail]` - 缩略图 URL
- `media[link]` - 链接附件 URL

## 适用场景

- 跨多个平台调度社交媒体帖子
- 管理社交媒体内容队列
- 分析跨渠道的帖子表现
- 自动化社交媒体发布工作流
- 协调团队社交媒体活动

## 速率限制

- 每个用户每分钟 60 个认证请求
- 超出限制返回 HTTP 429
- 联系 hello@buffer.com 可获取更高限制

## 相关技能

- social-media-calendar
- content-repurposing
- social-proof
- launch-sequence
