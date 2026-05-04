# Mention Me

企业级推荐营销平台，用于客户倡导计划。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API，用于推荐、客户、奖励管理 |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | - | JavaScript 小部件，用于嵌入 |

## 身份验证

- **类型**：API Key
- **请求头**：`Authorization: Bearer {api_key}`
- **环境**：沙箱和生产环境使用不同的密钥

## 常见 Agent 操作

### 创建推荐优惠

```bash
POST https://api.mention-me.com/api/v2/referrer-offer

{
  "email": "customer@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "order_number": "ORD-123",
  "order_total": 99.99,
  "order_currency": "USD"
}
```

### 获取客户的推荐链接

```bash
GET https://api.mention-me.com/api/v2/referrer/{customer_id}/share-links
```

### 记录被推荐人（被推荐的客户）

```bash
POST https://api.mention-me.com/api/v2/referee

{
  "email": "referred@example.com",
  "firstname": "Jane",
  "referrer_code": "JOHN123",
  "order_number": "ORD-456",
  "order_total": 149.99
}
```

### 获取推荐状态

```bash
GET https://api.mention-me.com/api/v2/referral/{referral_id}
```

### 列出客户的推荐记录

```bash
GET https://api.mention-me.com/api/v2/referrer/{customer_id}/referrals
```

### 获取奖励余额

```bash
GET https://api.mention-me.com/api/v2/referrer/{customer_id}/rewards
```

### 兑换奖励

```bash
POST https://api.mention-me.com/api/v2/referrer/{customer_id}/rewards/redeem

{
  "reward_id": "RWD-123",
  "order_number": "ORD-789"
}
```

## JavaScript 小部件

### 嵌入推荐小部件

```html
<div id="mmWrapper"></div>
<script>
  window.MentionMe = window.MentionMe || [];
  MentionMe.push({
    type: 'offer',
    customer: {
      email: 'customer@example.com',
      firstname: 'John',
      order_number: 'ORD-123'
    }
  });
</script>
<script src="https://tag.mention-me.com/client/{partner_code}.js" async></script>
```

### 姓名分享小部件

```javascript
MentionMe.push({
  type: 'nameShare',
  customer: {
    email: 'customer@example.com'
  }
});
```

## Webhook 事件

| 事件 | 触发时机 |
|-------|------|
| `referral.created` | 新推荐已追踪 |
| `referral.converted` | 被推荐人完成购买 |
| `reward.earned` | 奖励已解锁 |
| `reward.redeemed` | 奖励已使用 |

## 核心功能

- **A/B 测试** - 内置实验框架
- **欺诈预防** - 自动欺诈检测
- **多渠道** - 通过链接、邮件、社交分享
- **姓名分享** - 通过姓名而非代码推荐
- **细分** - 根据不同细分提供不同优惠
- **分析** - 推荐计划报告

## 关键对象

- **Referrer** - 进行推荐的客户
- **Referee** - 被推荐的客户
- **Referral** - 推荐人与被推荐人之间的关联
- **Offer** - 推荐计划配置
- **Reward** - 获得的激励

## 使用场景

- 企业级推荐计划
- 多市场推荐活动
- A/B 测试推荐优惠
- 防欺诈的推荐追踪
- 基于姓名的分享计划

## 速率限制

- 每分钟 1000 次请求
- 如需更高限制请联系

## 相关 Skills

- referral-program
- pricing-strategy
- analytics-tracking
