# GA4 实施参考

Google Analytics 4 的详细实施指南。

## 目录
- 配置（数据流、增强型测量事件、推荐事件）
- 自定义事件（gtag.js 实现、Google Tag Manager）
- 转化设置（创建转化、转化价值）
- 自定义维度和指标（何时使用、设置步骤、示例）
- 受众群体（创建受众群体、受众群体示例）
- 调试（DebugView、实时报告、常见问题）
- 数据质量（过滤器、跨域跟踪、会话设置）
- 与 Google Ads 集成（链接、受众群体导出）

## 配置

### 数据流

- 每个平台一个数据流（Web、iOS、Android）
- 启用增强型测量以进行自动跟踪
- 配置数据保留（默认 2 个月，最长 14 个月）
- 启用 Google Signals（用于跨设备跟踪，需获得同意）

### 增强型测量事件（自动）

| 事件 | 描述 | 配置 |
|-------|-------------|---------------|
| page_view | 页面加载 | 自动 |
| scroll | 90% 滚动深度 | 开启/关闭 |
| outbound_click | 点击外部域名 | 自动 |
| site_search | 使用搜索查询 | 配置参数 |
| video_engagement | YouTube 视频播放 | 开启/关闭 |
| file_download | PDF、文档等 | 可配置扩展名 |

### 推荐事件

尽可能使用 Google 预定义的事件以获得增强的报告功能：

**所有媒体资源：**
- login, sign_up
- share
- search

**电子商务：**
- view_item, view_item_list
- add_to_cart, remove_from_cart
- begin_checkout
- add_payment_info
- purchase, refund

**游戏：**
- level_up, unlock_achievement
- post_score, spend_virtual_currency

参考：https://support.google.com/analytics/answer/9267735

---

## 自定义事件

### gtag.js 实现

```javascript
// 基本事件
gtag('event', 'signup_completed', {
  'method': 'email',
  'plan': 'free'
});

// 带值的事件
gtag('event', 'purchase', {
  'transaction_id': 'T12345',
  'value': 99.99,
  'currency': 'USD',
  'items': [{
    'item_id': 'SKU123',
    'item_name': 'Product Name',
    'price': 99.99
  }]
});

// 用户属性
gtag('set', 'user_properties', {
  'user_type': 'premium',
  'plan_name': 'pro'
});

// 用户 ID（适用于已登录用户）
gtag('config', 'GA_MEASUREMENT_ID', {
  'user_id': 'USER_ID'
});
```

### Google Tag Manager（dataLayer）

```javascript
// 自定义事件
dataLayer.push({
  'event': 'signup_completed',
  'method': 'email',
  'plan': 'free'
});

// 设置用户属性
dataLayer.push({
  'user_id': '12345',
  'user_type': 'premium'
});

// 电子商务购买
dataLayer.push({
  'event': 'purchase',
  'ecommerce': {
    'transaction_id': 'T12345',
    'value': 99.99,
    'currency': 'USD',
    'items': [{
      'item_id': 'SKU123',
      'item_name': 'Product Name',
      'price': 99.99,
      'quantity': 1
    }]
  }
});

// 发送前清除 ecommerce（最佳实践）
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'view_item',
  'ecommerce': {
    // ...
  }
});
```

---

## 转化设置

### 创建转化

1. **收集事件** - 确保事件在 GA4 中触发
2. **标记为转化** - 管理 > 事件 > 标记为转化
3. **设置计数方法**：
   - 每次会话一次（潜在客户、注册）
   - 每个事件（购买）
4. **导入到 Google Ads** - 用于转化优化出价

### 转化价值

```javascript
// 带转化价值的事件
gtag('event', 'purchase', {
  'value': 99.99,
  'currency': 'USD'
});
```

或在 GA4 管理后台标记转化时设置默认值。

---

## 自定义维度和指标

### 何时使用

**自定义维度：**
- 想要按此细分/过滤的属性
- 用户属性（套餐类型、行业）
- 内容属性（作者、类别）

**自定义指标：**
- 要聚合的数值
- 分数、计数、持续时间

### 设置步骤

1. 管理 > 数据显示 > 自定义定义
2. 创建维度或指标
3. 选择范围：
   - **事件**：每个事件（content_type）
   - **用户**：每个用户（account_type）
   - **商品**：每个产品（product_category）
4. 输入参数名称（必须与事件参数匹配）

### 示例

| 维度 | 范围 | 参数 | 描述 |
|-----------|-------|-----------|-------------|
| 用户类型 | 用户 | user_type | 免费、试用、付费 |
| 内容作者 | 事件 | author | 博客文章作者 |
| 产品类别 | 商品 | item_category | 电子商务类别 |

---

## 受众群体

### 创建受众群体

管理 > 数据显示 > 受众群体

**用例：**
- 再营销受众群体（导出到 Ads）
- 细分分析
- 基于触发器的事件

### 受众群体示例

**高意向访客：**
- 查看了定价页面
- 未转化
- 在过去 7 天内

**活跃用户：**
- 3+ 次会话
- 或总互动时间 5+ 分钟

**购买者：**
- 购买事件
- 用于排除或类似受众

---

## 调试

### DebugView

启用方式：
- URL 参数：`?debug_mode=true`
- Chrome 扩展：GA Debugger
- gtag：配置中的 `'debug_mode': true`

查看位置：报告 > 配置 > DebugView

### 实时报告

在 30 分钟内检查事件：
报告 > 实时

### 常见问题

**事件未显示：**
- 首先检查 DebugView
- 验证 gtag/GTM 是否触发
- 检查过滤器排除项

**参数值缺失：**
- 未创建自定义维度
- 参数名称不匹配
- 数据仍在处理中（24-48 小时）

**转化未记录：**
- 事件未标记为转化
- 事件名称不匹配
- 计数方法（一次 vs. 每次）

---

## 数据质量

### 过滤器

管理 > 数据流 > [数据流] > 配置代码设置 > 定义内部流量

**排除：**
- 内部 IP 地址
- 开发者流量
- 测试环境

### 跨域跟踪

对于共享分析数据的多个域名：

1. 管理 > 数据流 > [数据流] > 配置代码设置
2. 配置你的域名
3. 列出所有应共享会话的域名

### 会话设置

管理 > 数据流 > [数据流] > 配置代码设置

- 会话超时（默认 30 分钟）
- 活跃会话持续时间（默认 10 秒）

---

## 与 Google Ads 集成

### 链接

1. 管理 > 产品链接 > Google Ads 链接
2. 在 Google Ads 中启用自动标记
3. 在 Google Ads 中导入转化

### 受众群体导出

在 GA4 中创建的受众群体可用于 Google Ads：
- 再营销活动
- 客户匹配
- 类似受众
