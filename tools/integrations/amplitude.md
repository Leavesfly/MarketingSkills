# Amplitude

产品分析平台，用于用户行为、留存率和实验分析。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | HTTP API（事件）、User Profile API、Export API |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | ✓ | JavaScript、iOS、Android、Python 等 |

## 认证

- **HTTP API**: API Key（事件追踪为公开）
- **Export/Dashboard API**: API Key + Secret Key

## 常用 Agent 操作

### 追踪事件

```bash
POST https://api2.amplitude.com/2/httpapi

{
  "api_key": "{api_key}",
  "events": [{
    "user_id": "user_123",
    "event_type": "signup_completed",
    "event_properties": {
      "plan": "pro"
    },
    "user_properties": {
      "email": "user@example.com"
    }
  }]
}
```

### 批量事件

```bash
POST https://api2.amplitude.com/batch

{
  "api_key": "{api_key}",
  "events": [
    {"user_id": "user_1", "event_type": "pageview"},
    {"user_id": "user_2", "event_type": "signup"}
  ]
}
```

### 获取用户活动

```bash
GET https://amplitude.com/api/2/useractivity?user={user_id}

Authorization: Basic {base64(api_key:secret_key)}
```

### 导出事件

```bash
GET https://amplitude.com/api/2/export?start=20240101T00&end=20240131T23

Authorization: Basic {base64(api_key:secret_key)}
```

### 获取留存数据

```bash
GET https://amplitude.com/api/2/retention?e={"event_type":"signup_completed"}&start=20240101&end=20240131

Authorization: Basic {base64(api_key:secret_key)}
```

### 使用 SQL 查询（Snowflake）

对于拥有 SQL 访问权限的 Amplitude 客户：
```sql
SELECT event_type, COUNT(*) as count
FROM events
WHERE event_time > '2024-01-01'
GROUP BY event_type
```

## JavaScript SDK

```javascript
// 初始化
amplitude.init('API_KEY');

// 识别用户
amplitude.setUserId('user_123');

// 设置用户属性
const identify = new amplitude.Identify();
identify.set('plan', 'pro');
amplitude.identify(identify);

// 追踪事件
amplitude.track('Feature Used', {
  feature_name: 'export'
});
```

## 关键概念

- **Events** - 带属性的用户行为
- **User Properties** - 持久化用户属性
- **Cohorts** - 行为细分群体
- **Funnels** - 多步骤转化分析
- **Retention** - 用户回访模式
- **Journeys** - 用户路径分析

## 适用场景

- 追踪产品分析数据
- 分析用户漏斗
- 队列分析和留存分析
- 实验和 A/B 测试
- 用户旅程映射

## 速率限制

- HTTP API：每秒 1000 个事件
- Export API：每小时 360 个请求

## 相关技能

- analytics-tracking
- ab-test-setup
- onboarding-cro
