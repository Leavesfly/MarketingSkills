# AI 图像提示词指南

如何为 AI 图像生成模型（Gemini/Nano Banana、Flux、Ideogram、DALL-E、Midjourney）编写有效的提示词。

---

## 提示词结构

一个优秀的图像提示词遵循以下公式：

```
[主体] + [场景/上下文] + [视觉风格] + [光线] + [构图] + [技术规格]
```

### 按使用场景划分的示例提示词

**博客头图 — SaaS 产品：**
```
A clean workspace with a laptop displaying a colorful analytics dashboard,
minimalist desk with a coffee cup and notebook,
bright natural window lighting from the right,
shallow depth of field, commercial photography style,
1200x630, high resolution
```

**社交媒体图形 — 公告：**
```
Abstract flowing gradient in deep purple and electric blue,
geometric shapes forming a network pattern,
dramatic rim lighting on edges,
modern tech aesthetic, clean and minimal,
1080x1080, vibrant colors
```

**产品生活方式拍摄：**
```
A person in a modern office smiling while looking at a tablet,
showing a project management interface on screen,
warm candid photography, natural lighting,
medium shot, shallow depth of field, editorial style
```

**个人资料横幅 — 专业：**
```
Wide panoramic abstract background in navy blue and teal,
subtle geometric grid pattern with soft gradient,
clean corporate aesthetic, muted lighting,
1584x396, no text, space for logo overlay on left三分之
```

**目录列表 — Product Hunt：**
```
Product screenshot on a clean gradient background,
soft shadow underneath, slight 3D perspective tilt,
modern SaaS product presentation style,
1270x760, bright and professional
```

---

## 风格关键词

### 照片级真实感
- "商业摄影"
- "Canon EOS R5 拍摄"
- "编辑风格"
- "自然光线"
- "浅景深"

### 简洁/企业风格
- "简洁现代美学"
- "极简设计"
- "专业企业风格"
- "明亮通透"
- "白色背景"

### 插画风格
- "扁平矢量插画"
- "等距 3D 渲染"
- "手绘素描风格"
- "水彩插画"
- "线条艺术"

### 抽象/品牌风格
- "流动渐变"
- "几何图案"
- "抽象数据可视化"
- "粒子效果"
- "全息虹彩"

### 科技/SaaS 风格
- "深色模式 UI 美学"
- "霓虹点缀光线"
- "玻璃拟态"
- "未来主义极简"
- "开发者导向"

---

## 光线关键词

| 术语 | 效果 | 适用场景 |
|------|--------|----------|
| **自然光** | 温暖、有机感 | 生活方式、编辑风格 |
| **影棚光线** | 均匀、可控 | 产品拍摄 |
| **轮廓光** | 边缘高光、戏剧性 | 头图、抽象图像 |
| **柔和定向光** | 柔和阴影、立体感 | 博客标题图 |
| **体积光** | 光束、氛围感 | 戏剧性、电影感 |
| **平面/均匀光** | 无阴影、干净 | 图标、图表 |
| **黄金时刻** | 温暖橙色调 | 生活方式、户外 |
| **高调光** | 明亮、极少阴影 | 简洁、企业风格 |

---

## 构图关键词

| 术语 | 效果 | 适用场景 |
|------|--------|----------|
| **三分法** | 主体偏离中心 | 编辑风格、生活方式 |
| **居中** | 主体在中间 | 产品拍摄、图标 |
| **宽幅/全景** | 广阔视野 | 横幅、标题图 |
| **特写/微距** | 细节聚焦 | 纹理、产品细节 |
| **鸟瞰/俯视** | 自上而下视角 | 桌面布置、平铺拍摄 |
| **留白** | 为文字叠加留出空间 | 博客标题图、横幅 |
| **对称** | 平衡、正式 | 企业风格、奢华感 |

---

## 模型特定技巧

### Gemini Image（Google）

- 营销图像的全能选择 — 质量好，价格合理
- 支持**图像编辑** — 上传现有图像并描述更改
- 文本渲染能力不错 — 可以处理简短标题
- 指定"高分辨率"以获得最佳输出
- 适用于详细、描述性的提示词
- 与文本生成使用相同的 API — 易于集成

### Flux（Black Forest Labs）

- **多图像参考**是杀手级功能 — 上传产品截图、品牌资产或风格参考
- 最适合在一组图像中保持**品牌一致性**
- 使用 Flux Pro 生成最终资产，使用 Flux Dev 进行快速迭代
- Flux Klein 用于高容量批量生成（最便宜）
- 通过参考图像进行风格迁移 > 提示词中的风格关键词
- 提示词可以比其他模型更短 — 参考图像承担主要工作

### Ideogram

- **最佳文本渲染**能力（行业领先的准确性）
- 当需要在图像中包含标题、标语或品牌名称时使用
- 风格参考系统（最多 3 张图像）用于品牌一致性
- 支持"Magic Prompt"自动增强
- 保持文本请求简单 — 最多 3-5 个词以确保可靠性
- 最适合需要内置文本的社交媒体图形和横幅

### GPT Image（OpenAI）

- 当前模型：`gpt-image-1` 及变体（DALL-E 3 已弃用）
- 与 ChatGPT 集成 — 对话式图像生成
- 擅长遵循详细的提示词
- 文本渲染能力不错（落后于 Ideogram，与 Gemini 相当）
- 自动提示词重写 — 可能偏离确切请求
- 最适合通过 ChatGPT 界面快速生成一次性图像
- API 比 ChatGPT 界面提供更多控制

### Midjourney

- 为艺术/编辑图像提供最高的美学质量
- 没有官方 API — 基于 Discord 或 Web 界面
- **不适合代理使用** — 仅用于手动创意探索
- 风格标志：`--style raw` 用于较少风格化，`--ar 16:9` 用于宽高比
- 最适合纯视觉质量最重要的头图
- V6+ 改进了文本渲染，但仍不可靠

---

## 常见提示词错误

| 错误 | 失败原因 | 修正方法 |
|---------|-------------|-----|
| "一张专业的图像" | 没有视觉细节 | 描述主体、场景、风格、光线 |
| 图像中长段落文字 | 模型无法渲染段落 | 最多 3-5 个词；后期添加文字 |
| "让它看起来好看" | 不可操作 | 指定风格："商业摄影，明亮" |
| 200+ 词的提示词 | 模型失去焦点 | 40-80 词，具体胜过全面 |
| 没有宽高比 | 随机输出尺寸 | 始终指定尺寸或比例 |
| "右下角放 Logo" | 放置不可靠 | 在后处理中添加 Logo |
| "让它病毒式传播" | 不是视觉指令 | 描述你想要的美学效果 |
| 请求 UI 截图 | AI 会虚构界面 | 改为捕获真实截图 |

---

## 批量生成工作流

当你需要多个风格一致的图像时（例如博客系列或社交活动）：

1. **生成 3-4 张测试图像**，使用不同的风格提示词
2. **根据品牌契合度选择获胜风格**
3. **保存确切的提示词**作为模板
4. **使用 Flux 多参考** — 上传获胜图像作为风格参考
5. **批量生成**变体，保持相同风格，改变主体
6. **后处理** — 添加文字叠加、Logo，裁剪到平台尺寸

---

## 宽高比快速参考

| 使用场景 | 比例 | 像素 | 说明 |
|----------|-------|--------|-------|
| 博客头图 / OG 图像 | 1.91:1 | 1200x630 | 通用 Web 标准 |
| 全宽头图 | 16:9 | 1920x1080 | 网站标题 |
| Instagram Feed | 1:1 | 1080x1080 | 正方形 |
| Instagram Feed（竖版） | 4:5 | 1080x1350 | 更多屏幕空间 |
| Stories / Reels | 9:16 | 1080x1920 | 垂直全屏 |
| LinkedIn 封面 | 4:1 | 1584x396 | 个人资料 |
| Twitter/X 标题 | 3:1 | 1500x500 | 资料横幅 |
| Product Hunt 图库 | 5:3 | 1270x760 | 发布页面 |
| GitHub 社交预览 | 2:1 | 1280x640 | 仓库链接卡片 |

---

## 成本优化

- **先以低质量迭代** — 使用 Flux Dev 或 Gemini Flash 制作草稿，最终版本再升级
- **使用参考而非长提示词** — Flux 多参考用更少的重试次数产生更一致的结果
- **批量处理相似请求** — 在一次会话中使用相同风格生成所有博客头图
- **缓存和重用** — 抽象背景、图案和纹理可以在多个图像中重用
- **后处理而非重新生成** — 在代码中裁剪、叠加文字和调整颜色，而不是生成新图像
