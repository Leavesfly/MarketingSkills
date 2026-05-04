# 转化跟踪设置

如何在各个广告平台设置转化跟踪像素。本指南涵盖安装、事件配置和验证——确保营销人员能够正确归因广告支出所需的一切。

---

## 为什么这很重要

如果没有转化跟踪：
- 广告平台无法针对你的实际目标进行优化
- 你对 ROAS 和 CPA 一无所知
- 无法构建再营销受众
- 你会在无法转化的展示上浪费预算

在投放广告之前，先做好跟踪设置。

---

## 平台像素概览

| 平台 | 像素/标签名称 | 事件 API | 关键事件 |
|----------|---------------|:----------:|------------|
| **Google Ads** | Google 标签（gtag.js） | Enhanced Conversions | purchase、sign_up、generate_lead |
| **Meta** | Meta Pixel + CAPI | Conversions API | Purchase、Lead、ViewContent、AddToCart |
| **LinkedIn** | Insight Tag | Conversions API | conversion（基于 URL 或事件） |
| **TikTok** | TikTok Pixel | Events API | Purchase、ViewContent、AddToCart、CompleteRegistration |
| **Twitter/X** | Twitter Pixel | - | Purchase、SignUp、Download |

---

## Google Ads

### 安装 Google 标签

添加到每个页面的 `<head>` 中：

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=AW-XXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'AW-XXXXXXXXX');
</script>
```

将 `AW-XXXXXXXXX` 替换为来自 Google Ads > 工具 > 转化的转化 ID。

### 设置转化操作

在 Google Ads > 目标 > 转化 > 新建转化操作中：

| 转化 | 类别 | 价值 | 计数 |
|-----------|----------|-------|-------|
| 购买 | 购买 | 动态（订单价值） | 每次 |
| 注册 / 潜在客户 | 注册 | 固定（$X 估计价值） | 一次 |
| 演示请求 | 潜在客户 | 固定（$X 估计价值） | 一次 |
| 免费试用开始 | 注册 | 固定（$X 估计价值） | 一次 |

### 触发转化事件

```javascript
// 购买
gtag('event', 'conversion', {
  'send_to': 'AW-XXXXXXXXX/CONVERSION_LABEL',
  'value': 99.00,
  'currency': 'USD',
  'transaction_id': 'ORDER-123'
});

// 潜在客户 / 注册
gtag('event', 'conversion', {
  'send_to': 'AW-XXXXXXXXX/CONVERSION_LABEL',
  'value': 50.00,
  'currency': 'USD'
});
```

### Enhanced Conversions

发送哈希处理的第一方数据（电子邮件、电话）以在 Cookie 限制后改善归因。在 Google Ads > 目标 > 设置 > Enhanced conversions 中启用。

```javascript
gtag('set', 'user_data', {
  'email': 'user@example.com',      // 由 gtag 自动哈希
  'phone_number': '+11234567890'
});
```

### Google Tag Manager 替代方案

如果使用 GTM 而不是内联 gtag.js：
1. 在所有页面上安装 GTM 容器
2. 在 GTM 中创建 Google Ads 转化标签
3. 为转化事件设置触发器（表单提交、购买）
4. 使用数据层传递动态值（订单金额、交易 ID）
5. 发布前使用 GTM 预览模式进行测试

---

## Meta（Facebook/Instagram）

### 安装 Meta Pixel

添加到每个页面的 `<head>` 中：

```html
<script>
  !function(f,b,e,v,n,t,s)
  {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
  n.callMethod.apply(n,arguments):n.queue.push(arguments)};
  if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
  n.queue=[];t=b.createElement(e);t.async=!0;
  t.src=v;s=b.getElementsByTagName(e)[0];
  s.parentNode.insertBefore(t,s)}(window, document,'script',
  'https://connect.facebook.net/en_US/fbevents.js');
  fbq('init', 'YOUR_PIXEL_ID');
  fbq('track', 'PageView');
</script>
```

从 Meta Events Manager 替换 `YOUR_PIXEL_ID`。

### 标准事件

```javascript
// 查看产品或关键页面
fbq('track', 'ViewContent', {
  content_name: 'Pro Plan',
  content_category: 'Pricing',
  value: 29.00,
  currency: 'USD'
});

// 潜在客户捕获（表单提交、演示请求）
fbq('track', 'Lead', {
  content_name: 'Demo Request',
  value: 50.00,
  currency: 'USD'
});

// 购买
fbq('track', 'Purchase', {
  value: 99.00,
  currency: 'USD',
  content_type: 'product',
  contents: [{ id: 'pro-plan', quantity: 1 }]
});

// 加入购物车（电子商务）
fbq('track', 'AddToCart', {
  content_ids: ['SKU-123'],
  content_type: 'product',
  value: 49.00,
  currency: 'USD'
});
```

### Conversions API（CAPI）

与像素并行工作的服务器端跟踪。在 iOS 14+ 和 Cookie 限制后准确跟踪所必需。

通过以下方式设置：
- **直接集成** — 从你的服务器向 Meta 的 API 发送事件
- **合作伙伴集成** — Shopify、WooCommerce、Segment 等具有内置 CAPI 支持
- **Conversions API Gateway** — Meta 通过 AWS 提供的托管解决方案

关键：同时从像素（浏览器）和 CAPI（服务器）发送相同的事件，并使用共享的 `event_id` 进行去重。

### Aggregated Event Measurement

iOS 14+ 跟踪所必需。在 Events Manager > Aggregated Event Measurement 中：
1. 验证你的域名
2. 按业务重要性顺序配置并优先处理你的前 8 个事件
3. 购买通常应为 #1，潜在客户 #2

---

## LinkedIn

### 安装 Insight Tag

添加到每个页面的 `</body>` 之前：

```html
<script type="text/javascript">
  _linkedin_partner_id = "YOUR_PARTNER_ID";
  window._linkedin_data_partner_ids = window._linkedin_data_partner_ids || [];
  window._linkedin_data_partner_ids.push(_linkedin_partner_id);
  (function(l) {
    if (!l){window.lintrk = function(a,b){window.lintrk.q.push([a,b])};
    window.lintrk.q=[]}
    var s = document.getElementsByTagName("script")[0];
    var b = document.createElement("script");
    b.type = "text/javascript";b.async = true;
    b.src = "https://snap.licdn.com/li.lms-analytics/insight.min.js";
    s.parentNode.insertBefore(b, s);})(window.lintrk);
</script>
```

### 转化跟踪

LinkedIn 支持两种方法：

**基于 URL**：当有人访问特定 URL（例如 `/thank-you`）时触发。
在 Campaign Manager > 分析 > 转化跟踪 > 创建转化中设置。

**基于事件**：在特定操作上手动触发：

```javascript
window.lintrk('track', { conversion_id: YOUR_CONVERSION_ID });
```

### LinkedIn CAPI

对于服务器端跟踪，LinkedIn 提供 Conversions API。通过合作伙伴集成（Segment、Tealium）或直接 API 调用设置。如果配置正确，会自动与 Insight Tag 去重。

---

## TikTok

### 安装 TikTok Pixel

添加到每个页面的 `<head>` 中：

```html
<script>
  !function (w, d, t) {
    w.TiktokAnalyticsObject=t;var ttq=w[t]=w[t]||[];
    ttq.methods=["page","track","identify","instances","debug","on","off",
    "once","ready","alias","group","enableCookie","disableCookie","holdConsent",
    "revokeConsent","grantConsent"],ttq.setAndDefer=function(t,e)
    {t[e]=function(){t.push([e].concat(Array.prototype.slice.call(arguments,0)))}};
    for(var i=0;i<ttq.methods.length;i++)ttq.setAndDefer(ttq,ttq.methods[i]);
    ttq.instance=function(t){for(var e=ttq._i[t]||[],n=0;
    n<ttq.methods.length;n++)ttq.setAndDefer(e,ttq.methods[n]);return e};
    ttq.load=function(e,n){var r="https://analytics.tiktok.com/i18n/pixel/events.js",
    o=n&&n.partner;ttq._i=ttq._i||{},ttq._i[e]=[],ttq._i[e]._u=r,
    ttq._t=ttq._t||{},ttq._t[e]=+new Date,ttq._o=ttq._o||{},
    ttq._o[e]=n||{};var s=document.createElement("script");
    s.type="text/javascript",s.async=!0,s.src=r+"?sdkid="+e+"&lib="+t;
    var a=document.getElementsByTagName("script")[0];
    a.parentNode.insertBefore(s,a)};
    ttq.load('YOUR_PIXEL_ID');
    ttq.page();
  }(window, document, 'ttq');
</script>
```

### 标准事件

```javascript
// 查看内容
ttq.track('ViewContent', {
  content_id: 'pro-plan',
  content_type: 'product',
  content_name: 'Pro Plan',
  value: 29.00,
  currency: 'USD'
});

// 完成注册 / 注册
ttq.track('CompleteRegistration', {
  content_name: 'Free Trial'
});

// 购买
ttq.track('Purchase', {
  content_id: 'pro-plan',
  content_type: 'product',
  value: 99.00,
  currency: 'USD',
  quantity: 1
});

// 加入购物车
ttq.track('AddToCart', {
  content_id: 'SKU-123',
  content_type: 'product',
  value: 49.00,
  currency: 'USD'
});
```

### Events API（服务器端）

TikTok 的 Events API 类似于 Meta 的 CAPI — 从你的服务器发送相同的事件以获得更好的归因。使用 `event_id` 与浏览器像素事件去重。

### Advanced Matching

传递哈希处理的用户数据以获得更好的归因：

```javascript
ttq.identify({
  email: 'user@example.com',       // 自动哈希
  phone_number: '+11234567890'
});
```

---

## 验证清单

安装任何像素后，在上线前进行验证：

### 浏览器端检查

- [ ] 像素在每个页面上触发（通过浏览器扩展检查）
- [ ] 转化事件在正确的时刻触发（在确认操作后，而不是在按钮点击时）
- [ ] 事件参数包含正确的值（货币、金额、内容 ID）
- [ ] 同一操作上没有重复触发事件
- [ ] 事件在桌面和移动设备上都触发

### 平台端检查

- [ ] 事件出现在平台的事件管理器/诊断中
- [ ] 测试转化显示正确的值
- [ ] 事件匹配质量可接受（Meta：分数 > 6）
- [ ] 服务器端事件正在与浏览器事件去重（不重复计数）

### 调试工具

| 平台 | 工具 |
|----------|------|
| Google | Google Tag Assistant、Chrome DevTools Network 标签 |
| Meta | Meta Pixel Helper（Chrome 扩展）、Events Manager Test Events |
| LinkedIn | Campaign Manager 中的 Insight Tag Validator |
| TikTok | TikTok Pixel Helper（Chrome 扩展）、Events Manager |
| 全部 | GTM Preview Mode（如果使用 Google Tag Manager） |

---

## 常见错误

- **在按钮点击时触发购买事件而不是确认付款** — 始终在成功/感谢页面或服务器确认后触发
- **像素和服务器事件之间缺少去重** — 如果没有共享的 `event_id`，你会重复计算转化
- **未在移动设备上测试** — 许多像素在移动浏览器或应用内 webview 中会中断
- **硬编码测试值** — 上线前删除测试交易金额
- **忘记排除内部流量** — 你团队的访问会夸大转化数据
- **在没有同意管理的情况下安装像素** — GDPR/CCPA 要求在适用区域触发跟踪像素之前获得用户同意
- **安装了像素但没有创建转化操作** — 像素收集数据，但如果没有定义的转化操作，广告平台将无法优化

---

## 何时使用服务器端跟踪

由于以下原因，仅浏览器的跟踪越来越不可靠：
- iOS 14+ App Tracking Transparency
- 第三方 Cookie 弃用
- 广告拦截器（30%+ 的技术受众）

**在以下情况下使用服务器端（CAPI/Events API）：**
- 投放 Meta 或 TikTok 广告（强烈推荐）
- 你的受众精通技术（更高的广告拦截器使用率）
- 你需要准确的购买/收入归因
- 你在任何平台上的每月支出 >$5K

**服务器端是可选的，当：**
- 仅投放 Google Ads（Enhanced Conversions 覆盖了大部分差距）
- 低广告支出 / 测试阶段
- B2B 仅使用 LinkedIn（Insight Tag 仍然可靠）
