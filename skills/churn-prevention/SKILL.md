---
name: churn-prevention
description: "当用户想要减少流失、构建取消流程、设置挽留优惠、恢复失败付款或实施留存策略时使用。也适用于用户提到'流失'、'取消流程'、'离站'、'挽留优惠'、'催款'、'失败付款恢复'、'赢回'、'留存'、'退出调查'、'暂停订阅'、'非自愿流失'、'用户一直在取消'、'流失率太高'、'如何留住用户'或'客户正在流失'等情况。每当有人失去订阅者或想要构建防止系统时使用。对于取消后的赢回邮件序列，请参阅 email-sequence。对于应用内升级付费墙，请参阅 paywall-upgrade-cro。"
metadata:
  version: 1.1.0
---

# 流失预防

你是 SaaS 留存和流失预防专家。你的目标是通过精心设计的取消流程、动态挽留优惠、主动留存和催款策略来帮助减少自愿流失（客户选择取消）和非自愿流失（付款失败）。

## 开始之前

**首先检查产品营销上下文：**
如果存在 `.agents/product-marketing-context.md`（或在旧设置中为 `.claude/product-marketing-context.md`），请在提问前阅读它。使用该上下文，仅询问未涵盖或特定于此任务的信息。

收集以下上下文（如未提供则询问）：

### 1. 当前流失情况
- 你的月度流失率是多少？（如果知道，区分自愿与非自愿）
- 有多少活跃订阅者？
- 每客户平均 MRR 是多少？
- 你今天有取消流程吗，还是取消会立即生效？

### 2. 计费与平台
- 使用什么计费提供商？（Stripe、Chargebee、Paddle、Recurly、Braintree）
- 月度、年度或两者兼有计费周期？
- 是否支持计划暂停或降级？
- 有任何现有留存工具吗？（Churnkey、ProsperStack、Raaft）

### 3. 产品与使用数据
- 你是否跟踪每个用户的功能使用情况？
- 你能识别参与度下降吗？
- 你有过去流失的取消原因数据吗？
- 你的激活指标是什么？（留存用户做了什么而流失用户没有做的？）

### 4. 约束条件
- B2B 还是 B2C？（影响流程设计）
- 是否需要自助取消？（某些法规要求轻松取消）
- 离站的品牌语调？（共情、直接、 playful）

---

## 此技能如何工作

流失有两种类型，需要不同的策略：

| 类型 | 原因 | 解决方案 |
|------|-------|----------|
| **自愿** | 客户选择取消 | 取消流程、挽留优惠、退出调查 |
| **非自愿** | 付款失败 | 催款邮件、智能重试、卡更新器 |

自愿流失通常占总流失的 50-70%。非自愿流失占 30-50%，但通常更容易修复。

此技能支持三种模式：

1. **构建取消流程** — 从头设计，包含调查、挽留优惠和确认
2. **优化现有流程** — 分析取消数据并提高挽留率
3. **设置催款** — 通过重试和邮件序列恢复失败付款

---

## 取消流程设计

### 取消流程结构

每个取消流程遵循以下顺序：

```
触发 → 调查 → 动态优惠 → 确认 → 取消后
```

**步骤 1：触发**
客户在账户设置中点击"取消订阅"。

**步骤 2：退出调查**
询问他们取消的原因。这决定了显示哪个挽留优惠。

**步骤 3：动态挽留优惠**
根据他们的原因提供有针对性的优惠（折扣、暂停、降级等）

**步骤 4：确认**
如果他们仍想取消，清晰地确认并附带计费周期结束消息。

**步骤 5：取消后**
设定期望，提供简单的重新激活路径，触发赢回序列。

### 退出调查设计

退出调查是基础。良好的原因类别：

| 原因 | 它告诉你什么 |
|--------|-------------------|
| 太贵了 | 价格敏感度，可能对折扣或降级有反应 |
| 使用不够频繁 | 参与度低，可能对暂停或入门帮助有反应 |
| 缺少某个功能 | 产品差距，展示路线图或变通方案 |
| 切换到竞争对手 | 竞争压力，了解他们提供什么 |
| 技术问题 / bug | 产品质量，升级到支持团队 |
| 临时 / 季节性需求 | 使用模式，提供暂停 |
| 业务关闭 / 变更 | 不可避免，学习并优雅放手 |
| 其他 | 包罗万象，包含自由文本字段 |

**调查最佳实践：**
- 1 个问题，单选加可选自由文本
- 最多 5-8 个原因选项（避免决策疲劳）
- 将最常见的原因放在前面（每季度审查数据）
- 不要让它感觉像内疚之旅
- "帮助我们改进"的框架比"你为什么要离开？"效果更好

### 动态挽留优惠

关键洞察：**将优惠与原因匹配。** 折扣不会挽救不使用产品的用户。功能路线图不会挽救负担不起的用户。

**优惠与原因映射：**

| 取消原因 | 主要优惠 | 备用优惠 |
|---------------|---------------|----------------|
| 太贵了 | 折扣（2-3 个月 20-30%） | 降级到更低计划 |
| 使用不够频繁 | 暂停（1-3 个月） | 免费入门会话 |
| 缺少功能 | 路线图预览 + 时间表 | 变通方案指南 |
| 切换到竞争对手 | 竞争对比 + 折扣 | 反馈会话 |
| 技术问题 | 立即升级到支持团队 | 积分 + 优先修复 |
| 临时 / 季节性 | 暂停订阅 | 临时降级 |
| 业务关闭 | 跳过优惠（尊重情况） | — |

### 挽留优惠类型

**折扣**
- 2-3 个月 20-30% 折扣是甜蜜点
- 避免 50%+ 折扣（训练客户为优惠而取消）
- 限时优惠（"此优惠在你离开此页面时过期"）
- 显示节省的美元金额，而不仅仅是百分比

**暂停订阅**
- 最多暂停 1-3 个月（更长的暂停很少重新激活）
- 60-80% 的暂停用户最终会返回活跃状态
- 自动重新激活并提前通知邮件
- 保持他们的数据和设置完整

**计划降级**
- 提供更低层级而不是完全取消
- 显示他们保留什么 vs 失去什么
- 定位为"调整你的计划大小"而不是"降级"
- 准备好时轻松升级回来

**功能解锁 / 扩展**
- 解锁他们尚未尝试的高级功能
- 扩展更高层级的试用
- 最适合"没有得到足够价值"的原因

**个人外展**
- 针对高价值账户（按 MRR 排名前 10-20%）
- 路由到客户成功进行通话
- 小公司的创始人个人邮件

### 取消流程 UI 模式

```
┌─────────────────────────────────────┐
│  我们很遗憾看到你离开          │
│                                     │
│  你取消的主要原因是      │
│  什么？                        │
│                                     │
│  ○ 太贵了                    │
│  ○ 使用不够频繁              │
│  ○ 缺少我需要的功能         │
│  ○ 切换到另一个工具        │
│  ○ 技术问题                 │
│  ○ 临时 / 现在不需要 │
│  ○ 其他：[____________]            │
│                                     │
│  [继续]                         │
│  [没关系，保留我的订阅] │
└─────────────────────────────────────┘
         ↓ （选择"太贵了"）
┌─────────────────────────────────────┐
│  如果我们可以帮忙呢？             │
│                                     │
│  我们很想留住你。这是一个    │
│  特别优惠：                     │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  接下来 3 个月享受 25% 折扣│  │
│  │  每月节省 $XX               │  │
│  │                               │  │
│  │  [接受优惠]               │  │
│  └───────────────────────────────┘  │
│                                     │
│  或者切换到 [基础计划]       │
│  $X/月 →                         │
│                                     │
│  [不，谢谢，继续取消]   │
└─────────────────────────────────────┘
```

**UI 原则：**
- 保持"继续取消"选项可见（无黑暗模式）
- 一个主要优惠 + 一个备用，而不是一堆选项
- 显示具体的美元节省，而不是抽象的百分比
- 尽可能使用客户的姓名和账户数据
- 移动友好（许多取消发生在移动端）

有关按行业和计费提供商划分的详细取消流程模式，请参阅 [references/cancel-flow-patterns.md](references/cancel-flow-patterns.md)。

---

## 流失预测与主动留存

最好的挽留发生在客户点击"取消"之前。

### 风险信号

跟踪这些流失的先导指标：

| 信号 | 风险级别 | 时间框架 |
|--------|-----------|-----------|
| 登录频率下降 50%+ | 高 | 取消前 2-4 周 |
| 关键功能使用停止 | 高 | 取消前 1-3 周 |
| 支持工单激增后停止 | 高 | 取消前 1-2 周 |
| 邮件打开率下降 | 中 | 取消前 2-6 周 |
| 计费页面访问增加 | 高 | 取消前几天 |
| 团队席位移除 | 高 | 取消前 1-2 周 |
| 数据导出启动 | 严重 | 取消前几天 |
| NPS 评分降至 6 以下 | 中 | 取消前 1-3 个月 |

### 健康评分模型

从加权信号构建一个简单的健康评分（0-100）：

```
健康评分 = (
  登录频率评分 × 0.30 +
  功能使用评分   × 0.25 +
  支持情感     × 0.15 +
  计费健康        × 0.15 +
  参与度评分      × 0.15
)
```

| 评分 | 状态 | 行动 |
|-------|--------|--------|
| 80-100 | 健康 | 追加销售机会 |
| 60-79 | 需要注意 | 主动检查 |
| 40-59 | 有风险 | 干预活动 |
| 0-39 | 严重 | 个人外展 |

### 主动干预

**在他们考虑取消之前：**

| 触发器 | 干预措施 |
|---------|-------------|
| 使用量下降 >50% 持续 2 周 | "我们注意到你尚未使用 [功能]。需要帮助吗？"邮件 |
| 接近计划限制 | 升级提示（不是墙 — paywall-upgrade-cro 处理这个） |
| 14 天未登录 | 重新参与邮件，附带最近产品更新 |
| NPS 贬损者（0-6） | 24 小时内个人跟进 |
| 支持工单未解决 >48 小时 | 升级 + 主动状态更新 |
| 年度续费在 30 天内 | 价值回顾邮件 + 续费确认 |

---

## 非自愿流失：付款恢复

失败付款导致所有流失的 30-50%，但最容易恢复。

### 催款堆栈

```
预催款 → 智能重试 → 催款邮件 → 宽限期 → 强制取消
```

### 预催款（预防失败）

- **卡到期提醒**：卡到期前 30、15 和 7 天发送邮件
- **备用付款方式**：注册时提示提供第二种付款方式
- **卡更新服务**：Visa/Mastercard 自动更新计划（减少硬拒绝 30-50%）
- **预计费通知**：年度计划扣费前 3-5 天发送邮件

### 智能重试逻辑

并非所有失败都相同。按拒绝类型制定重试策略：

| 拒绝类型 | 示例 | 重试策略 |
|-------------|----------|----------------|
| 软拒绝（临时） | 资金不足、处理器超时 | 7-10 天内重试 3-5 次 |
| 硬拒绝（永久） | 卡被盗、账户关闭 | 不要重试 — 要求新卡 |
| 需要身份验证 | 3D Secure、SCA | 发送客户更新付款 |

**重试时机最佳实践：**
- 重试 1：失败后 24 小时
- 重试 2：失败后 3 天
- 重试 3：失败后 5 天
- 重试 4：失败后 7 天（伴随催款邮件升级）
- 4 次重试后：强制取消并提供重新激活路径

**智能重试提示：** 在付款最初成功的月份日期重试（如果第 1 天之前成功，则在第 1 天重试）。Stripe Smart Retries 自动处理此问题。

### 催款邮件序列

| 邮件 | 时机 | 语调 | 内容 |
|-------|--------|------|---------|
| 1 | 第 0 天（失败） | 友好提醒 | "你的付款未成功。更新你的卡。" |
| 2 | 第 3 天 |  helpful 提醒 | "快速提醒 — 更新你的付款以保持访问权限。" |
| 3 | 第 7 天 | 紧急 | "你的账户将在 3 天后暂停。立即更新。" |
| 4 | 第 10 天 | 最后警告 | "保持账户活跃的最后机会。" |

**催款邮件最佳实践：**
- 直接链接到付款更新页面（如果可能，无需登录）
- 显示他们将失去什么（他们的数据、他们团队的访问权限）
- 不要责备（"你的付款失败"而不是"你未能付款"）
- 包含支持联系以获得帮助
- 纯文本在催款方面比设计邮件表现更好

### 恢复基准

| 指标 | 差 | 平均 | 好 |
|--------|------|---------|------|
| 软拒绝恢复 | <40% | 50-60% | 70%+ |
| 硬拒绝恢复 | <10% | 20-30% | 40%+ |
| 总体付款恢复 | <30% | 40-50% | 60%+ |
| 预催款预防 | 无 | 10-15% | 20-30% |

有关包含提供商特定设置的完整催款手册，请参阅 [references/dunning-playbook.md](references/dunning-playbook.md)。

---

## Metrics & Measurement

### Key Churn Metrics

| Metric | Formula | Target |
|--------|---------|--------|
| Monthly churn rate | Churned customers / Start-of-month customers | <5% B2C, <2% B2B |
| Revenue churn (net) | (Lost MRR - Expansion MRR) / Start MRR | Negative (net expansion) |
| Cancel flow save rate | Saved / Total cancel sessions | 25-35% |
| Offer acceptance rate | Accepted offers / Shown offers | 15-25% |
| Pause reactivation rate | Reactivated / Total paused | 60-80% |
| Dunning recovery rate | Recovered / Total failed payments | 50-60% |
| Time to cancel | Days from first churn signal to cancel | Track trend |

### Cohort Analysis

Segment churn by:
- **Acquisition channel** — Which channels bring stickier customers?
- **Plan type** — Which plans churn most?
- **Tenure** — When do most cancellations happen? (30, 60, 90 days?)
- **Cancel reason** — Which reasons are growing?
- **Save offer type** — Which offers work best for which segments?

### Cancel Flow A/B Tests

Test one variable at a time:

| Test | Hypothesis | Metric |
|------|-----------|--------|
| Discount % (20% vs 30%) | Higher discount saves more | Save rate, LTV impact |
| Pause duration (1 vs 3 months) | Longer pause increases return rate | Reactivation rate |
| Survey placement (before vs after offer) | Survey-first personalizes offers | Save rate |
| Offer presentation (modal vs full page) | Full page gets more attention | Save rate |
| Copy tone (empathetic vs direct) | Empathetic reduces friction | Save rate |

**How to run cancel flow experiments:** Use the **ab-test-setup** skill to design statistically rigorous tests. PostHog is a good fit for cancel flow experiments — its feature flags can split users into different flows server-side, and its funnel analytics track each step of the cancel flow (survey → offer → accept/decline → confirm). See the [PostHog integration guide](../../tools/integrations/posthog.md) for setup.

---

## Common Mistakes

- **No cancel flow at all** — Instant cancel leaves money on the table. Even a simple survey + one offer saves 10-15%
- **Making cancellation hard to find** — Hidden cancel buttons breed resentment and bad reviews. Many jurisdictions require easy cancellation (FTC Click-to-Cancel rule)
- **Same offer for every reason** — A blanket discount doesn't address "missing feature" or "not using it"
- **Discounts too deep** — 50%+ discounts train customers to cancel-and-return for deals
- **Ignoring involuntary churn** — Often 30-50% of total churn and the easiest to fix
- **No dunning emails** — Letting payment failures silently cancel accounts
- **Guilt-trip copy** — "Are you sure you want to abandon us?" damages brand trust
- **Not tracking save offer LTV** — A "saved" customer who churns 30 days later wasn't really saved
- **Pausing too long** — Pauses beyond 3 months rarely reactivate. Set limits.
- **No post-cancel path** — Make reactivation easy and trigger win-back emails, because some churned users will want to come back

---

## Tool Integrations

For implementation, see the [tools registry](../../tools/REGISTRY.md).

### Retention Platforms

| Tool | Best For | Key Feature |
|------|----------|-------------|
| **Churnkey** | Full cancel flow + dunning | AI-powered adaptive offers, 34% avg save rate |
| **ProsperStack** | Cancel flows with analytics | Advanced rules engine, Stripe/Chargebee integration |
| **Raaft** | Simple cancel flow builder | Easy setup, good for early-stage |
| **Chargebee Retention** | Chargebee customers | Native integration, was Brightback |

### Billing Providers (Dunning)

| Provider | Smart Retries | Dunning Emails | Card Updater |
|----------|:------------:|:--------------:|:------------:|
| **Stripe** | Built-in (Smart Retries) | Built-in | Automatic |
| **Chargebee** | Built-in | Built-in | Via gateway |
| **Paddle** | Built-in | Built-in | Managed |
| **Recurly** | Built-in | Built-in | Built-in |
| **Braintree** | Manual config | Manual | Via gateway |

### Related CLI Tools

| Tool | Use For |
|------|---------|
| `stripe` | Subscription management, dunning config, payment retries |
| `customer-io` | Dunning email sequences, retention campaigns |
| `posthog` | Cancel flow A/B tests via feature flags, funnel analytics |
| `mixpanel` / `ga4` | Usage tracking, churn signal analysis |
| `segment` | Event routing for health scoring |

---

## Related Skills

- **email-sequence**: For win-back email sequences after cancellation
- **paywall-upgrade-cro**: For in-app upgrade moments and trial expiration
- **pricing-strategy**: For plan structure and annual discount strategy
- **onboarding-cro**: For activation to prevent early churn
- **analytics-tracking**: For setting up churn signal events
- **ab-test-setup**: For testing cancel flow variations with statistical rigor
