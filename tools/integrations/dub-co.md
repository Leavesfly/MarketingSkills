# Dub.co

面向现代营销团队的链接管理和归因平台。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | 用于链接、分析、域名的 REST API |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | ✓ | 提供 TypeScript SDK |

## 认证

- **类型**：API Key
- **请求头**：`Authorization: Bearer {api_key}`
- **获取密钥**：Dub 仪表板中的 Settings > API Keys

## 常用 Agent 操作

### 创建短链接

```bash
POST https://api.dub.co/links

{
  "url": "https://example.com/landing-page",
  "domain": "link.example.com",
  "key": "summer-sale",
  "tags": ["campaign:summer", "channel:email"]
}
```

### 通过 key 获取链接

```bash
GET https://api.dub.co/links?domain=link.example.com&key=summer-sale
```

### 列出链接

```bash
GET https://api.dub.co/links?domain=link.example.com&page=1
```

### 获取链接分析数据

```bash
GET https://api.dub.co/analytics?domain=link.example.com&key=summer-sale&interval=30d
```

### 获取按位置划分的点击数据

```bash
GET https://api.dub.co/analytics/country?domain=link.example.com&key=summer-sale
```

### 获取按设备划分的点击数据

```bash
GET https://api.dub.co/analytics/device?domain=link.example.com&key=summer-sale
```

### 更新链接

```bash
PATCH https://api.dub.co/links/{link_id}

{
  "url": "https://example.com/new-landing-page",
  "tags": ["campaign:summer", "channel:social"]
}
```

### 删除链接

```bash
DELETE https://api.dub.co/links/{link_id}
```

### 批量创建链接

```bash
POST https://api.dub.co/links/bulk

[
  {"url": "https://example.com/page1", "key": "page1"},
  {"url": "https://example.com/page2", "key": "page2"}
]
```

## TypeScript SDK

### 安装

```bash
npm install dub
```

### 使用

```typescript
import { Dub } from "dub";

const dub = new Dub({ token: "YOUR_API_KEY" });

// Create link
const link = await dub.links.create({
  url: "https://example.com",
  domain: "link.example.com"
});

// Get analytics
const analytics = await dub.analytics.retrieve({
  domain: "link.example.com",
  key: "summer-sale"
});
```

## 关键特性

- **自定义域名** - 使用自己的品牌域名
- **链接分析** - 点击量、位置、设备、来源
- **标签** - 按活动、渠道等组织链接
- **二维码** - 为每个链接自动生成
- **密码保护** - 保护敏感链接
- **过期设置** - 限时链接
- **地理定位** - 基于位置重定向

## 分析维度

- `clicks` - 总点击次数
- `country` - 按国家划分的点击
- `city` - 按城市划分的点击
- `device` - 按设备类型划分的点击
- `browser` - 按浏览器划分的点击
- `os` - 按操作系统划分的点击
- `referer` - 按来源划分的点击

## 使用时机

- 创建可跟踪的营销链接
- 构建推荐链接系统
- 跟踪活动归因
- 通过链接进行落地页 A/B 测试
- 生成品牌短 URL
- 分析链接表现

## 速率限制

- 免费版：1,000 个链接，每秒 5 次 API 请求
- Pro 版：无限链接，每秒 50 次 API 请求
- 企业版：自定义限制

## 相关 Skills

- referral-program
- analytics-tracking
- paid-ads
