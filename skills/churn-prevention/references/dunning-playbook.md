# 催缴策略手册

恢复失败付款和减少非自愿流失的完整指南。

---

## 为什么催缴很重要

- 失败付款导致 30-50% 的所有订阅流失
- 大多数失败付款通过正确的策略可以恢复
- 订阅业务每年因非自愿流失损失估计达 1290 亿美元
- 有效的催缴可恢复 50-60% 的失败付款

---

## 催缴时间线

```
Day -30 to -7: Pre-dunning (prevent failures)
Day 0:         Payment fails → Smart retry #1 + Email #1
Day 1-3:       Smart retry #2 + Email #2
Day 3-5:       Smart retry #3
Day 5-7:       Smart retry #4 + Email #3
Day 7-10:      Final retry + Email #4 (final warning)
Day 10-14:     Grace period ends → Account paused/cancelled
Day 14+:       Win-back sequence begins
```

---

## 预催缴：在失败发生前预防

### 卡片过期管理

| 时间 | 操作 |
|--------|--------|
| 到期前 30 天 | 邮件："您尾号为 4242 的卡片下月到期" |
| 到期前 15 天 | 邮件："更新您的支付方式以避免中断" |
| 到期前 7 天 | 邮件："您的卡片将在 7 天后到期 — 立即更新" |
| 到期前 3 天 | 应用内横幅："支付方式即将到期" |

**邮件模板 — 卡片即将到期：**
```
Subject: Your card ending in 4242 expires soon

Hi [Name],

The card on file for your [Product] subscription expires on [date].

Update your payment method now to avoid any interruption:

[Update Payment Method →]

This takes less than 30 seconds.

— [Product] Team
```

### 卡片更新服务

主要卡网络提供自动卡片更新计划：

| 服务 | 网络 | 功能 |
|---------|---------|--------------|
| Visa Account Updater (VAU) | Visa | 自动更新存储的卡号和到期日期 |
| Mastercard Automatic Billing Updater (ABU) | Mastercard | Mastercard 相同功能 |
| Amex Cardrefresher | American Express | Amex 相同功能 |

**影响：** 将因过期/更换卡片导致的硬性拒绝减少 30-50%。

**如何启用：**
- **Stripe**：自动 — 默认启用
- **Chargebee**：通过网关设置启用
- **Recurly**：内置，默认启用
- **Braintree**：联系处理器以启用

### 备用支付方式

提示添加第二种支付方式：
- 注册期间："添加备用支付方式"（转化率较低）
- 首次成功付款后："用备用卡保护您的账户"（更好的时机）
- 失败付款恢复后："添加备用方式以防止未来中断"（最佳时机 — 他们感受到了痛苦）

### 预账单通知

对于年度计划或高价值订阅：
- 续费前 7 天发送包含金额和日期的邮件
- 包含更新支付方式的链接
- 显示续费包含的内容
- 某些自动续费法规要求

---

## 智能重试策略

### 拒绝类型分类

| 代码 | 类型 | 含义 | 重试？ |
|------|------|---------|--------|
| `insufficient_funds` | 软性 | 暂时余额不足 | 是 — 2-3 天后重试 |
| `card_declined`（通用） | 软性 | 各种临时原因 | 是 — 重试 3-4 次 |
| `processing_error` | 软性 | 网关/网络问题 | 是 — 24 小时内重试 |
| `expired_card` | 硬性 | 卡片已过期 | 否 — 请求新卡 |
| `stolen_card` | 硬性 | 卡片报告被盗 | 否 — 请求新卡 |
| `do_not_honor` | 软性/硬性 | 银行拒绝（模糊） | 再试一次，然后请求新卡 |
| `authentication_required` | 认证 | 需要 SCA/3DS | 发送客户进行认证 |

### 各提供商的重试计划

**Stripe（智能重试 — 推荐）：**
- 在 Stripe 仪表板 → Billing → Settings 中启用"Smart Retries"
- Stripe 的机器学习模型基于数十亿笔交易选择最佳重试时机
- 通常在 3-4 周内进行 4-8 次重试尝试
- 比固定计划重试多恢复约 15%

**手动重试计划（如果没有智能重试）：**

| 重试 | 时机 | 最佳日期/时间 |
|-------|--------|--------------|
| 1 | 第 1 天（失败后 24 小时） | 早上，与原始付款相同的星期几 |
| 2 | 第 3 天 | 尝试一天中的不同时间 |
| 3 | 第 5 天 | 典型发薪日之后（1 号、15 号） |
| 4 | 第 7 天 | 下一个工作日的早上 |
| 5（最终） | 第 10 天 | 宽限期结束前的最后一次尝试 |

**重试时机洞察：**
- 在原始付款成功的同一天重试
- 在常见发薪日之后重试（每月 1 号和 15 号）
- 避免在周末重试（批准率较低）
- 早上重试（当地时间 8-10 点）表现略好

---

## 催缴邮件序列

### 邮件 1：付款失败（第 0 天）

**语气：** 友好、实事求是。无警报。

```
Subject: Action needed — your payment didn't go through

Hi [Name],

We tried to charge your [card type] ending in [last 4] for your
[Product] subscription ($[amount]), but it didn't go through.

This happens sometimes — usually a quick card update fixes it.

[Update Payment Method →]

Your access isn't affected yet. We'll retry automatically, but
updating your card is the fastest fix.

Need help? Just reply to this email.

— [Product] Team
```

### 邮件 2：提醒（第 3 天）

**语气：** 有帮助，稍微紧急。

```
Subject: Quick reminder — update your payment for [Product]

Hi [Name],

Just a heads-up — we still haven't been able to process your
$[amount] payment for [Product].

[Update Payment Method →]

Takes less than 30 seconds. Your [data/projects/team access]
is safe, but we'll need a valid payment method to keep your
account active.

Questions? Reply here and we'll help.

— [Product] Team
```

### 邮件 3：紧急（第 7 天）

**语气：** 直接，明确后果。

```
Subject: Your [Product] account will be paused in 3 days

Hi [Name],

We've tried to process your payment several times, but your
[card type] ending in [last 4] keeps getting declined.

If we don't receive payment by [date], your account will be
paused and you'll lose access to:

• [Key feature/data they use]
• [Their projects/workspace]
• [Team access for X members]

[Update Payment Method Now →]

Your data won't be deleted — you can reactivate anytime by
updating your payment method.

— [Product] Team
```

### 邮件 4：最后警告（第 10 天）

**语气：** 最终、清晰、无责备。

```
Subject: Last chance to keep your [Product] account active

Hi [Name],

This is our last reminder. Your payment of $[amount] is past
due, and your account will be paused tomorrow ([date]).

[Update Payment Method →]

After pausing:
• Your data is saved for [90 days]
• You can reactivate anytime
• Just update your card to restore access

If you intended to cancel, no action needed — your account
will be paused automatically.

— [Product] Team
```

---

## 宽限期管理

### 宽限期内发生的事情

| 设置 | 建议 |
|---------|---------------|
| 持续时间 | 最终重试后 7-14 天 |
| 访问权限 | 降级（只读）或完全访问 |
| 可见性 | 应用内横幅："付款逾期 — 更新以继续" |
| 重试 | 宽限期内继续后台重试 |
| 沟通 | 催缴邮件继续发送 |

### 访问降级选项

**选项 A：宽限期内完全访问（B2B 推荐）**
- 摩擦更低，客户感到受尊重
- 更高的恢复率（他们仍然看到价值）
- 风险：一些客户会利用宽限期

**选项 B：只读访问（B2C 推荐）**
- 可以查看但不能创建/编辑
- 创造紧迫感而无需担心数据丢失
- 明确消息："更新付款以恢复完全访问"

**选项 C：立即锁定（不推荐）**
- 激进，损害关系
- 更低的恢复率
- 仅适用于非常低成本的计划

### 宽限期后

| 时间 | 操作 |
|--------|--------|
| 宽限期结束 | 暂停账户（不删除） |
| 暂停后第 1 天 | "您的账户已暂停"邮件 |
| 暂停后第 7 天 | "您的数据仍在这里"提醒 |
| 暂停后第 30 天 | 带有新优惠的赢回尝试 |
| 暂停后第 60 天 | 最终赢回 |
| 暂停后第 90 天 | 数据删除警告（如适用） |

---

## 特定提供商设置

### Stripe

**启用智能重试：**
1. 仪表板 → 设置 → Billing → 订阅和邮件
2. 在重试规则下启用"Smart Retries"
3. 在仪表板 → 设置 → 邮件中设置失败付款邮件

**自定义重试规则（如果不使用智能重试）：**
```
Retry 1: 3 days after failure
Retry 2: 5 days after failure
Retry 3: 7 days after failure
Final:   Mark subscription as unpaid after last retry
```

**要处理的 Webhook 事件：**
- `invoice.payment_failed` — 触发催缴
- `invoice.paid` — 取消催缴，恢复访问
- `customer.subscription.updated` — 状态更改
- `customer.subscription.deleted` — 最终取消

### Chargebee

**内置催缴：**
1. 设置 → 配置 Chargebee → 重试设置
2. 配置重试尝试和间隔
3. 设置 → 配置 Chargebee → 邮件通知 → 催缴

**催缴选项：**
- 可配置计划的自动重试
- 内置催缴邮件（可自定义模板）
- 每个计划的宽限期配置

### Paddle

**托管催缴：**
- Paddle 自动处理重试和催缴
- 有限的自定义（Paddle 管理关系）
- Webhook：`subscription.payment_failed`、`subscription.cancelled`
- 最适合免动手方法

### Recurly

**收入恢复：**
1. 配置 → 催缴管理
2. 为每个计划设置重试计划
3. 配置宽限期和最终操作（暂停 vs 取消）

**高级功能：**
- 机器学习重试优化
- 每个计划的催缴计划
- 内置账户更新器

---

## 应用内催缴

不要仅依赖邮件。在应用中显示付款失败：

### 横幅模式
```
┌──────────────────────────────────────────────────────┐
│ ⚠ Your payment of $29 failed. Update your card to    │
│ avoid losing access. [Update Payment →]  [Dismiss]   │
└──────────────────────────────────────────────────────┘
```

**规则：**
- 在催缴期间的每次页面加载时显示
- 允许关闭（但下次会话时再次显示）
- 直接链接到付款更新（尽可能少的点击）
- 不要阻止产品 — 让他们继续使用

### 模态框模式（用于最后警告）
```
┌─────────────────────────────────────┐
│                                     │
│  Your account will be paused        │
│  on [date]                          │
│                                     │
│  Update your payment method to      │
│  keep access to your [X] projects   │
│  and [Y] team members.              │
│                                     │
│  [Update Payment Method]            │
│  [Remind Me Later]                  │
│                                     │
└─────────────────────────────────────┘
```

---

## 衡量催缴绩效

### 关键指标

| 指标 | 计算方法 | 目标 |
|--------|-----------------|--------|
| 恢复率 | 恢复的付款 / 总失败 | 50-60% |
| 按拒绝类型的恢复率 | 每个类型的恢复 / 失败 | 软性：70%+，硬性：40%+ |
| 恢复时间 | 从失败到成功付款的天数 | <5 天 |
| 预催缴预防率 | 预防的失败 / 预期失败 | 20-30% |
| 催缴邮件打开率 | 每封邮件的打开 / 发送 | 60%+ |
| 催缴邮件点击率 | 每封邮件的点击 / 打开 | 30%+ |
| 月收入恢复 | 恢复付款金额的总和 | 跟踪趋势 |
| 非自愿流失损失的收入 | 失败 + 未恢复金额的总和 | 跟踪趋势 |

### 基准测试

**按公司阶段：**

| 阶段 | 典型非自愿流失 | 优化后目标 |
|-------|--------------------------|--------------------------|
| 早期（< 100 万美元 ARR） | 每月 MRR 的 3-5% | 1-2% |
| 增长期（100-1000 万美元 ARR） | 每月 MRR 的 2-4% | 0.5-1.5% |
| 规模期（1000 万+ 美元 ARR） | 每月 MRR 的 1-3% | 0.3-0.8% |

### ROI 计算

```
Monthly failed payment MRR:        $10,000
Current recovery rate:              30% ($3,000 recovered)
Target recovery rate:               60% ($6,000 recovered)
Monthly improvement:                $3,000/month
Annual improvement:                 $36,000/year
Cost of dunning optimization:       ~$200-500/month (tooling)
ROI:                                6-15x
```
