# 事件库参考

按业务类型和上下文划分的完整事件跟踪列表。

## 目录
- 营销网站事件（导航与互动、CTA 与表单交互、转化事件）
- 产品/应用事件（新手引导、核心使用、错误与支持）
- 货币化事件（定价与结账、订阅管理）
- 电子商务事件（浏览、购物车、结账、购买后）
- B2B / SaaS 特定事件（团队与协作、集成事件、账户事件）
- 事件属性（参数）
- 漏斗事件序列

## 营销网站事件

### 导航与互动

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| page_view | 页面加载（增强型） | page_title, page_location, content_group |
| scroll_depth | 用户滚动到阈值 | depth (25, 50, 75, 100) |
| outbound_link_clicked | 点击外部链接 | link_url, link_text |
| internal_link_clicked | 站内点击 | link_url, link_text, location |
| video_played | 视频开始播放 | video_id, video_title, duration |
| video_completed | 视频播放完成 | video_id, video_title, duration |

### CTA 与表单交互

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| cta_clicked | 点击行动号召按钮 | button_text, cta_location, page |
| form_started | 用户开始填写表单 | form_name, form_location |
| form_field_completed | 字段已填写 | form_name, field_name |
| form_submitted | 表单成功提交 | form_name, form_location |
| form_error | 表单验证失败 | form_name, error_type |
| resource_downloaded | 资源已下载 | resource_name, resource_type |

### 转化事件

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| signup_started | 开始注册 | source, page |
| signup_completed | 完成注册 | method, plan, source |
| demo_requested | 演示表单已提交 | company_size, industry |
| contact_submitted | 联系表单已发送 | inquiry_type |
| newsletter_subscribed | 邮件列表注册 | source, list_name |
| trial_started | 免费试用开始 | plan, source |

---

## 产品/应用事件

### 新手引导

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| signup_completed | 账户已创建 | method, referral_source |
| onboarding_started | 开始新手引导 | - |
| onboarding_step_completed | 步骤已完成 | step_number, step_name |
| onboarding_completed | 所有步骤完成 | steps_completed, time_to_complete |
| onboarding_skipped | 用户跳过新手引导 | step_skipped_at |
| first_key_action_completed | 达到"Aha"时刻 | action_type |

### 核心使用

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| session_started | 应用会话开始 | session_number |
| feature_used | 功能交互 | feature_name, feature_category |
| action_completed | 核心操作完成 | action_type, count |
| content_created | 用户创建内容 | content_type |
| content_edited | 用户修改内容 | content_type |
| content_deleted | 用户删除内容 | content_type |
| search_performed | 应用内搜索 | query, results_count |
| settings_changed | 设置已修改 | setting_name, new_value |
| invite_sent | 用户邀请他人 | invite_type, count |

### 错误与支持

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| error_occurred | 发生错误 | error_type, error_message, page |
| help_opened | 访问帮助 | help_type, page |
| support_contacted | 提出支持请求 | contact_method, issue_type |
| feedback_submitted | 用户反馈已提交 | feedback_type, rating |

---

## 货币化事件

### 定价与结账

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| pricing_viewed | 查看定价页面 | source |
| plan_selected | 选择套餐 | plan_name, billing_cycle |
| checkout_started | 开始结账 | plan, value |
| payment_info_entered | 提交支付信息 | payment_method |
| purchase_completed | 购买成功 | plan, value, currency, transaction_id |
| purchase_failed | 购买失败 | error_reason, plan |

### 订阅管理

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| trial_started | 试用开始 | plan, trial_length |
| trial_ended | 试用到期 | plan, converted (bool) |
| subscription_upgraded | 套餐升级 | from_plan, to_plan, value |
| subscription_downgraded | 套餐降级 | from_plan, to_plan |
| subscription_cancelled | 取消订阅 | plan, reason, tenure |
| subscription_renewed | 续订 | plan, value |
| billing_updated | 支付方式变更 | - |

---

## 电子商务事件

### 浏览

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| product_viewed | 查看产品页面 | product_id, product_name, category, price |
| product_list_viewed | 查看分类/列表页 | list_name, products[] |
| product_searched | 执行搜索 | query, results_count |
| product_filtered | 应用筛选 | filter_type, filter_value |
| product_sorted | 应用排序 | sort_by, sort_order |

### 购物车

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| product_added_to_cart | 添加商品 | product_id, product_name, price, quantity |
| product_removed_from_cart | 移除商品 | product_id, product_name, price, quantity |
| cart_viewed | 查看购物车页面 | cart_value, items_count |

### 结账

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| checkout_started | 开始结账 | cart_value, items_count |
| checkout_step_completed | 步骤完成 | step_number, step_name |
| shipping_info_entered | 输入地址 | shipping_method |
| payment_info_entered | 输入支付信息 | payment_method |
| coupon_applied | 使用优惠券 | coupon_code, discount_value |
| purchase_completed | 下单 | transaction_id, value, currency, items[] |

### 购买后

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| order_confirmed | 查看确认页面 | transaction_id |
| refund_requested | 发起退款 | transaction_id, reason |
| refund_completed | 退款处理完成 | transaction_id, value |
| review_submitted | 产品评价已提交 | product_id, rating |

---

## B2B / SaaS 特定事件

### 团队与协作

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| team_created | 创建新团队/组织 | team_size, plan |
| team_member_invited | 发送邀请 | role, invite_method |
| team_member_joined | 成员接受邀请 | role |
| team_member_removed | 成员被移除 | role |
| role_changed | 权限已更新 | user_id, old_role, new_role |

### 集成事件

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| integration_viewed | 查看集成页面 | integration_name |
| integration_started | 开始设置 | integration_name |
| integration_connected | 成功连接 | integration_name |
| integration_disconnected | 移除集成 | integration_name, reason |

### 账户事件

| 事件名称 | 描述 | 属性 |
|------------|-------------|------------|
| account_created | 创建新账户 | source, plan |
| account_upgraded | 套餐升级 | from_plan, to_plan |
| account_churned | 账户关闭 | reason, tenure, mrr_lost |
| account_reactivated | 客户回归 | previous_tenure, new_plan |

---

## 事件属性（参数）

### 要包含的标准属性

**用户上下文：**
```
user_id: "12345"
user_type: "free" | "trial" | "paid"
account_id: "acct_123"
plan_type: "starter" | "pro" | "enterprise"
```

**会话上下文：**
```
session_id: "sess_abc"
session_number: 5
page: "/pricing"
referrer: "https://google.com"
```

**活动上下文：**
```
source: "google"
medium: "cpc"
campaign: "spring_sale"
content: "hero_cta"
```

**产品上下文（电子商务）：**
```
product_id: "SKU123"
product_name: "Product Name"
category: "Category"
price: 99.99
quantity: 1
currency: "USD"
```

**时间：**
```
timestamp: "2024-01-15T10:30:00Z"
time_on_page: 45
session_duration: 300
```

---

## 漏斗事件序列

### 注册漏斗
1. signup_started
2. signup_step_completed (email)
3. signup_step_completed (password)
4. signup_completed
5. onboarding_started

### 购买漏斗
1. pricing_viewed
2. plan_selected
3. checkout_started
4. payment_info_entered
5. purchase_completed

### 电子商务漏斗
1. product_viewed
2. product_added_to_cart
3. cart_viewed
4. checkout_started
5. shipping_info_entered
6. payment_info_entered
7. purchase_completed
