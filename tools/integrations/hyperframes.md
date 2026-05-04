# Hyperframes

来自 HeyGen 的开源程序化视频框架。从 HTML/CSS/JS 创建视频——无需 React，无专有 DSL。专为 AI Agent 工作流设计。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | - | 库，非托管服务 |
| MCP | - | - |
| CLI | 是 | `npx hyperframes render` |
| SDK | 是 | Node.js/TypeScript 包 |

## 为什么选择 Hyperframes

- **LLM 原生**: AI 模型生成 HTML 比 React 组件更好——纯 Web 标准，无框架 DSL
- **确定性**: 相同输入始终产生相同输出（适合自动化）
- **开源**: Apache 2.0 许可证，零渲染费用
- **Agent 友好**: 任何能编写 HTML 的编码 Agent 都能创建视频

## 安装

```bash
npm install hyperframes
```

要求：Node.js 22+，Chrome/Chromium（用于渲染）

## 快速开始

```typescript
import { render } from "hyperframes";

await render({
  frames: [
    {
      html: `
        <div style="display:flex; align-items:center; justify-content:center;
                    height:100%; background:#000; color:#fff; font-family:system-ui;">
          <h1 style="font-size:64px;">Welcome to Acme</h1>
        </div>
      `,
      duration: 3,
    },
    {
      html: `
        <div style="display:flex; flex-direction:column; align-items:center;
                    justify-content:center; height:100%; background:#000; color:#fff;
                    font-family:system-ui;">
          <h2 style="font-size:48px;">Ship faster with AI</h2>
          <p style="font-size:24px; color:#888;">Try it free today</p>
        </div>
      `,
      duration: 3,
    },
  ],
  output: "intro.mp4",
  width: 1080,
  height: 1920, // 9:16 竖屏
  fps: 30,
});
```

## 核心概念

### 帧

每一帧都是在时间线特定点渲染的 HTML 文档。将其视为具有持续时间的幻灯片。

```typescript
{
  html: "<div>...</div>",  // 完整 HTML 内容
  duration: 3,              // 显示秒数
  css?: "body { ... }",     // 可选外部 CSS
}
```

### 过渡效果

CSS 过渡和动画在帧之间生效：

```html
<div style="animation: fadeIn 0.5s ease-in;">
  <h1>Slide In</h1>
</div>
<style>
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
</style>
```

### 数据驱动视频

从数据生成帧以进行批量制作：

```typescript
const features = ["Analytics", "Automation", "AI Insights"];

const frames = features.map((feature) => ({
  html: `
    <div style="display:flex; align-items:center; justify-content:center;
                height:100%; background:linear-gradient(135deg, #667eea, #764ba2);
                color:#fff; font-family:system-ui;">
      <h1 style="font-size:56px;">${feature}</h1>
    </div>
  `,
  duration: 2.5,
}));

await render({ frames, output: "features.mp4", width: 1080, height: 1920 });
```

## 常见营销模板

### 产品公告

```typescript
const frames = [
  { html: hookSlide("Something new is here"), duration: 2 },
  { html: featureSlide(title, description, screenshot), duration: 4 },
  { html: ctaSlide("Try it free →", url), duration: 3 },
];
```

### 推荐视频

```typescript
const frames = [
  { html: quoteSlide(testimonial.text), duration: 4 },
  { html: attributionSlide(testimonial.author, testimonial.company), duration: 2 },
  { html: ctaSlide("Join 1,000+ happy customers"), duration: 3 },
];
```

### 统计数据视频

```typescript
const metrics = [
  { label: "Users", value: "10,000+" },
  { label: "Uptime", value: "99.9%" },
  { label: "NPS", value: "72" },
];

const frames = metrics.map(m => ({
  html: metricSlide(m.label, m.value),
  duration: 2.5,
}));
```

## 宽高比

| 平台 | 宽度 | 高度 | 比例 |
|----------|-------|--------|-------|
| TikTok/Reels/Shorts | 1080 | 1920 | 9:16 |
| YouTube | 1920 | 1080 | 16:9 |
| Instagram Feed | 1080 | 1080 | 1:1 |
| Instagram Feed | 1080 | 1350 | 4:5 |

## Hyperframes vs. Remotion

| 因素 | Hyperframes | Remotion |
|--------|-------------|----------|
| 语言 | HTML/CSS/JS | React/TypeScript |
| Agent 兼容性 | 更好（纯 HTML） | 良好（需要 React 知识） |
| 动画 | CSS 过渡/关键帧 | Spring 物理、插值 |
| 云端渲染 | 无内置 | Lambda (AWS) |
| 许可证 | Apache 2.0（免费） | 商业用途需公司许可证 |
| 生态系统 | 新兴、增长中 | 成熟、大型社区 |

**使用 Hyperframes 的场景：** AI Agent 生成视频、简单动画、批量模板化内容、成本敏感。

**使用 Remotion 的场景：** 需要复杂动画、已在使用 React、需要 Lambda 实现大规模、想要更大的生态系统。

## 相关技能

- video
- social-content
- ad-creative
