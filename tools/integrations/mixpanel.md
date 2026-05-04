# Mixpanel

产品分析平台，用于追踪用户行为和留存率。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | Ingestion API、Query API、数据导出 |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | ✓ | JavaScript、iOS、Android、Python 等 |

## 身份验证

- **Ingestion**：Project token（公开）
- **Query API**：Service Account（username:secret 作为 Basic auth）
- **Export**：API Secret

## 常见 Agent 操作

### 追踪事件（Ingestion API）

```bash
POST https://api.mixpanel.com/track

{
  "event": "signup_completed",
  "properties": {
    "token": "{project_token}",
    "distinct_id": "user_123",
    "plan": "pro",
    "time": 1705312800
  }
}
```

### 设置用户画像

```bash
POST https://api.mixpanel.com/engage

{
  "$token": "{project_token}",
  "$distinct_id": "user_123",
  "$set": {
    "$email": "user@example.com",
    "$name": "John Doe",
    "plan": "pro"
  }
}
```

### 查询事件（Query API）

```bash
POST https://mixpanel.com/api/2.0/insights

{
  "project_id": {project_id},
  "bookmark_id": null,
  "params": {
    "events": [{"event": "signup_completed"}],
    "time_range": {
      "from_date": "2024-01-01",
      "to_date": "2024-01-31"
    }
  }
}
```

### 获取漏斗数据

```bash
GET https://mixpanel.com/api/2.0/funnels?funnel_id={funnel_id}&from_date=2024-01-01&to_date=2024-01-31
```

### 导出原始事件

```bash
GET https://data.mixpanel.com/api/2.0/export?from_date=2024-01-01&to_date=2024-01-01
```

### 获取留存数据

```bash
GET https://mixpanel.com/api/2.0/retention?from_date=2024-01-01&to_date=2024-01-31&retention_type=birth&born_event=signup_completed
```

## JavaScript SDK

```javascript
// 初始化
mixpanel.init('YOUR_TOKEN');

// 识别用户
mixpanel.identify('user_123');

// 设置用户属性
mixpanel.people.set({
  '$email': 'user@example.com',
  'plan': 'pro'
});

// 追踪事件
mixpanel.track('Feature Used', {
  'feature_name': 'export'
});
```

## 核心概念

- **Events** - 用户行为（注册、购买等）
- **Properties** - 事件的属性
- **User Profiles** - 持久化用户数据
- **Cohorts** - 保存的用户细分
- **Funnels** - 转化序列
- **Retention** - 用户回访模式

## 使用场景

- 追踪产品使用事件
- 分析转化漏斗
- 衡量功能采用情况
- 留存分析
- 用户细分

## 速率限制

- Ingestion：无硬性限制（建议批量）
- Query API：根据套餐而定

## 相关 Skills

- analytics-tracking
- ab-test-setup
- onboarding-cro
