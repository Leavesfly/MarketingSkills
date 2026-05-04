# Google Tag Manager 实施参考

通过 Google Tag Manager 实施跟踪的详细指南。

## 目录
- 容器结构（代码标签、触发器、变量）
- 命名约定
- 数据层模式
- 常见代码标签配置（GA4 配置代码标签、GA4 事件代码标签、Facebook 像素）
- 预览和调试
- 工作区和版本控制
- 同意管理
- 高级模式（代码标签序列、异常处理、自定义 JavaScript 变量）

## 容器结构

### 代码标签

代码标签是在触发时执行的代码片段。

**常见代码标签类型：**
- GA4 配置（基础设置）
- GA4 事件（自定义事件）
- Google Ads 转化
- Facebook 像素
- LinkedIn Insight Tag
- 自定义 HTML（用于其他像素）

### 触发器

触发器定义代码标签何时触发。

**内置触发器：**
- 页面浏览：所有页面、DOM 就绪、窗口加载完成
- 点击：所有元素、仅链接
- 表单提交
- 滚动深度
- 计时器
- 元素可见性

**自定义触发器：**
- 自定义事件（来自 dataLayer）
- 触发器组（多个条件）

### 变量

变量捕获动态值。

**内置（按需启用）：**
- 点击文本、点击 URL、点击 ID、点击类
- 页面路径、页面 URL、页面主机名
- 引用页
- 表单元素、表单 ID

**用户定义：**
- 数据层变量
- JavaScript 变量
- 查找表
- 正则表达式表
- 常量

---

## 命名约定

### 推荐格式

```
[类型] - [描述] - [详情]

代码标签：
GA4 - 事件 - 注册完成
GA4 - 配置 - 基础配置
FB - 像素 - 页面浏览
HTML - LiveChat 小部件

触发器：
点击 - CTA 按钮
提交 - 联系表单
查看 - 定价页面
自定义 - signup_completed

变量：
DL - user_id
JS - 当前时间戳
LT - 活动来源映射
```

---

## 数据层模式

### 基本结构

```javascript
// 初始化（在 GTM 之前的 <head> 中）
window.dataLayer = window.dataLayer || [];

// 推送事件
dataLayer.push({
  'event': 'event_name',
  'property1': 'value1',
  'property2': 'value2'
});
```

### 页面加载数据

```javascript
// 在页面加载时设置（在 GTM 容器之前）
window.dataLayer = window.dataLayer || [];
dataLayer.push({
  'pageType': 'product',
  'contentGroup': 'products',
  'user': {
    'loggedIn': true,
    'userId': '12345',
    'userType': 'premium'
  }
});
```

### 表单提交

```javascript
document.querySelector('#contact-form').addEventListener('submit', function() {
  dataLayer.push({
    'event': 'form_submitted',
    'formName': 'contact',
    'formLocation': 'footer'
  });
});
```

### 按钮点击

```javascript
document.querySelector('.cta-button').addEventListener('click', function() {
  dataLayer.push({
    'event': 'cta_clicked',
    'ctaText': this.innerText,
    'ctaLocation': 'hero'
  });
});
```

### 电子商务事件

```javascript
// 产品浏览
dataLayer.push({ ecommerce: null }); // 清除之前的
dataLayer.push({
  'event': 'view_item',
  'ecommerce': {
    'items': [{
      'item_id': 'SKU123',
      'item_name': 'Product Name',
      'price': 99.99,
      'item_category': 'Category',
      'quantity': 1
    }]
  }
});

// 添加到购物车
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'add_to_cart',
  'ecommerce': {
    'items': [{
      'item_id': 'SKU123',
      'item_name': 'Product Name',
      'price': 99.99,
      'quantity': 1
    }]
  }
});

// 购买
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'purchase',
  'ecommerce': {
    'transaction_id': 'T12345',
    'value': 99.99,
    'currency': 'USD',
    'tax': 5.00,
    'shipping': 10.00,
    'items': [{
      'item_id': 'SKU123',
      'item_name': 'Product Name',
      'price': 99.99,
      'quantity': 1
    }]
  }
});
```

---

## 常见代码标签配置

### GA4 配置代码标签

**代码标签类型：** Google Analytics: GA4 Configuration

**设置：**
- 测量 ID：G-XXXXXXXX
- 发送页面浏览：勾选（用于页面浏览）
- 用户属性：添加任何用户级维度

**触发器：** 所有页面

### GA4 事件代码标签

**代码标签类型：** Google Analytics: GA4 Event

**设置：**
- 配置代码标签：选择你的配置代码标签
- 事件名称：{{DL - event_name}} 或硬编码
- 事件参数：从 dataLayer 添加参数

**触发器：** 自定义事件，匹配事件名称

### Facebook 像素 - 基础

**代码标签类型：** 自定义 HTML

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

**触发器：** 所有页面

### Facebook 像素 - 事件

**代码标签类型：** 自定义 HTML

```html
<script>
  fbq('track', 'Lead', {
    content_name: '{{DL - form_name}}'
  });
</script>
```

**触发器：** 自定义事件 - form_submitted

---

## 预览和调试

### 预览模式

1. 在 GTM 中点击"预览"
2. 输入网站 URL
3. GTM 调试面板在底部打开

**检查内容：**
- 此事件触发的代码标签
- 未触发的代码标签（及原因）
- 变量及其值
- 数据层内容

### 调试技巧

**代码标签未触发：**
- 检查触发器条件
- 验证 dataLayer 推送
- 检查代码标签序列

**变量值错误：**
- 检查 dataLayer 结构
- 验证变量路径（嵌套对象）
- 检查时序（数据可能尚不存在）

**多次触发：**
- 检查触发器唯一性
- 查找重复的代码标签
- 检查代码标签触发选项

---

## 工作区和版本控制

### 工作区

使用工作区进行团队协作：
- 默认工作区用于生产环境
- 大型变更使用单独的工作区
- 准备就绪后合并

### 版本管理

**最佳实践：**
- 为每个版本命名描述性名称
- 添加说明变更的注释
- 发布前审查变更
- 记录生产版本

**版本注释示例：**
```
v15: 添加了购买转化跟踪
- 新代码标签：GA4 - 事件 - 购买
- 新触发器：自定义事件 - purchase
- 新变量：DL - transaction_id, DL - value
- 已测试：Chrome、Safari、移动端
```

---

## 同意管理

### 同意模式集成

```javascript
// 默认状态（同意前）
gtag('consent', 'default', {
  'analytics_storage': 'denied',
  'ad_storage': 'denied'
});

// 同意时更新
function grantConsent() {
  gtag('consent', 'update', {
    'analytics_storage': 'granted',
    'ad_storage': 'granted'
  });
}
```

### GTM 同意概览

1. 在管理后台启用同意概览
2. 为每个代码标签配置同意
3. 代码标签自动尊重同意状态

---

## 高级模式

### 代码标签序列

**设置按顺序触发的代码标签：**
代码标签配置 > 高级设置 > 代码标签序列

**用例：**
- 配置代码标签在事件代码标签之前
- 像素初始化在跟踪之前
- 转化后清理

### 异常处理

**触发器异常** - 防止代码标签触发：
- 排除某些页面
- 排除内部流量
- 测试期间排除

### 自定义 JavaScript 变量

```javascript
// 获取 URL 参数
function() {
  var params = new URLSearchParams(window.location.search);
  return params.get('campaign') || '(not set)';
}

// 获取 Cookie 值
function() {
  var match = document.cookie.match('(^|;) ?user_id=([^;]*)(;|$)');
  return match ? match[2] : null;
}

// 从页面获取数据
function() {
  var el = document.querySelector('.product-price');
  return el ? parseFloat(el.textContent.replace('$', '')) : 0;
}
```
