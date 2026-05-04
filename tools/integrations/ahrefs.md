# Ahrefs

SEO 工具集，用于反向链接分析、关键词研究和竞争研究。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API，支持 Site Explorer、Keywords Explorer |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | - | 仅 API |

## 认证

- **类型**: API Token
- **请求头**: `Authorization: Bearer {api_token}`
- **获取令牌**: 在 Ahrefs 仪表板的账户设置 > API 中获取

## 常用 Agent 操作

### 域名评级

```bash
GET https://api.ahrefs.com/v3/site-explorer/domain-rating?target=example.com

Authorization: Bearer {api_token}
```

### 反向链接概览

```bash
GET https://api.ahrefs.com/v3/site-explorer/backlinks-stats?target=example.com&mode=domain

Authorization: Bearer {api_token}
```

### 引用域

```bash
GET https://api.ahrefs.com/v3/site-explorer/refdomains?target=example.com&mode=domain&limit=100

Authorization: Bearer {api_token}
```

### 反向链接列表

```bash
GET https://api.ahrefs.com/v3/site-explorer/backlinks?target=example.com&mode=domain&limit=100

Authorization: Bearer {api_token}
```

### 自然搜索关键词

```bash
GET https://api.ahrefs.com/v3/site-explorer/organic-keywords?target=example.com&mode=domain&country=us&limit=100

Authorization: Bearer {api_token}
```

### 热门页面

```bash
GET https://api.ahrefs.com/v3/site-explorer/top-pages?target=example.com&mode=domain&country=us&limit=50

Authorization: Bearer {api_token}
```

### 关键词概览

```bash
GET https://api.ahrefs.com/v3/keywords-explorer/overview?keywords=keyword1,keyword2&country=us

Authorization: Bearer {api_token}
```

### 关键词建议

```bash
GET https://api.ahrefs.com/v3/keywords-explorer/matching-terms?keyword=seed+keyword&country=us&limit=100

Authorization: Bearer {api_token}
```

### SERP 概览

```bash
GET https://api.ahrefs.com/v3/keywords-explorer/serp-overview?keyword=target+keyword&country=us

Authorization: Bearer {api_token}
```

## 关键指标

### 域名指标
- `domain_rating` - 域名评级（DR）
- `ahrefs_rank` - Ahrefs 排名
- `referring_domains` - 引用域数量
- `backlinks` - 总反向链接数
- `organic_traffic` - 预估自然流量

### 关键词指标
- `volume` - 月搜索量
- `keyword_difficulty` - KD 分数（0-100）
- `cpc` - 每次点击费用
- `clicks` - 预估月点击次数
- `global_volume` - 全球搜索量

### 反向链接字段
- `url_from` - 来源 URL
- `url_to` - 目标 URL
- `anchor` - 锚文本
- `domain_rating_source` - 来源 DR
- `first_seen` - 首次发现日期

## 模式

- `domain` - 整个域名
- `subdomains` - 域名 + 子域名
- `prefix` - URL 前缀
- `exact` - 精确 URL

## 适用场景

- 反向链接分析
- 外链建设研究
- 关键词研究
- 竞争分析
- 内容差距分析
- 网站审计

## 速率限制

- 根据套餐而异
- 每个请求 500-5000 行

## 相关技能

- seo-audit
- content-strategy
- competitor-alternatives
