# 广告创意的生成式 AI 工具

使用 AI 图像生成器、视频生成器和基于代码的视频工具大规模制作广告视觉素材的参考。

---

## 何时使用生成式工具

| 需求 | 工具类别 | 最佳选择 |
|------|---------------|----------|
| 静态广告图片（横幅、社交） | 图像生成 | Nano Banana Pro、Flux、Ideogram |
| 带文字叠加的广告图片 | 图像生成（支持文字） | Ideogram、Nano Banana Pro |
| 短视频广告（6-30 秒） | 视频生成 | Veo、Kling、Runway、Sora、Seedance |
| 带配音的视频广告 | 视频生成 + 语音 | Veo/Sora（原生），或 Runway + ElevenLabs |
| 广告配音轨道 | 语音生成 | ElevenLabs、OpenAI TTS、Cartesia |
| 多语言广告版本 | 语音生成 | ElevenLabs、PlayHT |
| 品牌声音克隆 | 语音生成 | ElevenLabs、Resemble AI |
| 产品模型和变体 | 图像生成 + 参考 | Flux（多图像参考） |
| 规模化模板视频广告 | 基于代码的视频 | Remotion |
| 个性化视频（姓名、数据） | 基于代码的视频 | Remotion |
| 品牌一致的变体 | 图像生成 + 样式参考 | Flux、Ideogram、Nano Banana Pro |

---

## 图像生成

### Nano Banana Pro（Gemini）

Google DeepMind 的图像生成模型，可通过 Gemini API 使用。

**最适合：** 高质量广告图片、产品视觉效果、文字渲染
**API：** Gemini API（Google AI Studio、Vertex AI）
**定价：** ~$0.04/图片（Gemini 2.5 Flash Image），~$0.24/4K 图片（Nano Banana Pro）

**优势：**
- 强大的图像文字渲染能力（标志、标题）
- 原生图像编辑（用提示修改现有图像）
- 通过用于文本生成的同一 Gemini API 可用
- 在一个模型中支持生成和编辑

**广告创意用例：**
- 从文本描述生成社交媒体广告图片
- 创建产品模型变体
- 编辑现有广告图片（交换背景、更改颜色）
- 生成内置标题文字的图片

**API 示例：**
```bash
# Using the Gemini API for image generation
curl -X POST "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-image:generateContent" \
  -H "Content-Type: application/json" \
  -H "x-goog-api-key: $GEMINI_API_KEY" \
  -d '{
    "contents": [{"parts": [{"text": "Create a clean, modern social media ad image for a project management tool. Show a laptop with a kanban board interface. Bright, professional, 16:9 ratio."}]}],
    "generationConfig": {"responseModalities": ["TEXT", "IMAGE"]}
  }'
```

**文档：** [Gemini Image Generation](https://ai.google.dev/gemini-api/docs/image-generation)

---

### Flux（Black Forest Labs）

开放权重图像生成模型，可通过 Replicate 和 BFL 的原生 API 访问。

**最适合：** 逼真图像、品牌一致的变体、多参考生成
**API：** Replicate、BFL API、fal.ai
**定价：** ~$0.01-0.06/图片，取决于模型和分辨率

**模型变体：**
| 模型 | 速度 | 质量 | 成本 | 最适合 |
|-------|-------|---------|------|----------|
| Flux 2 Pro | ~6 秒 | 最高 | $0.015/MP | 最终生产资产 |
| Flux 2 Flex | ~22 秒 | 高 + 编辑 | $0.06/MP | 迭代编辑 |
| Flux 2 Dev | ~2.5 秒 | 良好 | $0.012/MP | 快速原型设计 |
| Flux 2 Klein | 最快 | 良好 | 最低 | 大批量批量生成 |

**优势：**
- 多图像参考（最多 8 张图像）以实现跨广告的一致身份
- 产品一致性 — 同一产品在不同上下文中
- 从参考图像进行样式迁移
- 开放权重 Dev 模型用于自托管

**广告创意用例：**
- 生成 50+ 个具有一致产品/人物身份的广告变体
- 创建上下文中的产品图片（你的 SaaS 在不同设备上）
- 使用参考图像与现有品牌资产进行样式匹配
- 快速 A/B 测试图片变体

**文档：** [Replicate Flux](https://replicate.com/black-forest-labs/flux-2-pro)、[BFL API](https://docs.bfl.ml/)

---

### Ideogram

专注于图像中的排版和文字渲染。

**最适合：** 带文字的广告横幅、品牌图形、带标题的社交广告图片
**API：** Ideogram API、Runware
**定价：** ~$0.06/图片（API），~$0.009/图片（订阅）

**优势：**
- 同类最佳的文字渲染（~90% 准确率，而大多数工具为 ~30%）
- 样式参考系统（上传最多 3 张参考图像）
- 43 亿种样式预设以实现一致的品牌美学
- 擅长标志和品牌排版

**广告创意用例：**
- 直接在图像中生成带标题文字的广告横幅
- 创建带有品牌文字叠加的社交媒体图形
- 生成具有 consistent 排版的多种设计变体
- 生成促销材料，无需为每次迭代聘请设计师

**文档：** [Ideogram API](https://developer.ideogram.ai/)、[Ideogram](https://ideogram.ai/)

---

### 其他图像工具

| 工具 | 最适合 | API 状态 | 说明 |
|------|----------|------------|-------|
| **DALL-E 3**（OpenAI） | 通用图像生成 | 官方 API | 与 ChatGPT 集成，良好的文字渲染 |
| **Midjourney** | 艺术性、高美学图像 | 无官方公共 API | 基于 Discord；存在非官方 API 但有被封禁风险 |
| **Stable Diffusion** | 自托管、可定制 | 开源 | 最适合拥有 GPU 基础设施的团队 |

---

## 视频生成

### Google Veo

Google DeepMind 的视频生成模型，可通过 Gemini API 和 Vertex AI 使用。

**最适合：** 带原生音频的高质量视频广告、社交垂直视频
**API：** Gemini API、Vertex AI
**定价：** ~$0.15/秒（Veo 3.1 Fast），~$0.40/秒（Veo 3.1 Standard）

**功能：**
- 1080p 下最长 60 秒
- 原生音频生成（对话、音效、环境音）
- 垂直 9:16 输出用于 Stories/Reels/Shorts
- 升级到 4K
- 文本到视频和图像到视频

**广告创意用例：**
- 从文本描述生成短视频广告（15-30 秒）
- 为 TikTok、Reels、Shorts 创建垂直视频广告
- 制作带配音的产品演示
- 从同一提示生成具有不同样式的多个视频变体

**文档：** [Veo on Vertex AI](https://cloud.google.com/vertex-ai/generative-ai/docs/video/overview)

---

### Kling（快手）

具有同步音视频生成和相机控制的视频生成。

**最适合：** 电影感视频广告、较长形式内容、音频同步视频
**API：** Kling API、PiAPI、fal.ai
**定价：** ~$0.09/秒（通过 fal.ai 第三方）

**功能：**
- 1080p/30-48fps 下最长 3 分钟
- 同步音视频生成（Kling 2.6）
- 文本到视频和图像到视频
- 运动和相机控制

**广告创意用例：**
- 较长的产品解释视频
- 带同步音频的电影感品牌视频
- 将产品图片动画化为视频广告

**文档：** [Kling AI Developer](https://klingai.com/global/dev/model/video)

---

### Runway

具有强大可控性的视频生成和编辑平台。

**最适合：** 受控视频生成、样式一致的内容、编辑现有素材
**API：** Runway Developer Portal

**功能：**
- Gen-4：跨镜头的角色/场景一致性
- 运动笔刷和相机控制
- 带参考图像的图像到视频
- 视频到视频样式迁移

**广告创意用例：**
- 生成跨场景具有 consistent 角色/产品的视频广告
- 样式迁移现有素材以匹配品牌美学
- 扩展或混音现有视频内容

**文档：** [Runway API](https://docs.dev.runwayml.com/)

---

### Sora 2（OpenAI）

OpenAI 的带同步音频的视频生成模型。

**最适合：** 带对话和声音的高保真视频
**API：** OpenAI API
**定价：** 提供免费层；Pro 从 $0.10-0.50/秒，取决于分辨率

**功能：**
- 带同步音频最长 60 秒
- 对话、音效和环境音频
- sora-2（快速）和 sora-2-pro（质量）变体
- 文本到视频和图像到视频

**广告创意用例：**
- 视频推荐和谈话头风格广告
- 带叙述的产品演示视频
- 叙事品牌视频

**文档：** [OpenAI Video Generation](https://platform.openai.com/docs/guides/video-generation)

---

### Seedance 2.0（字节跳动）

字节跳动的具有同步音视频生成和多模态输入的视频生成模型。

**最适合：** 快速、实惠的带原生音频的视频广告、多模态参考输入
**API：** BytePlus（官方）、Replicate、WaveSpeedAI、fal.ai（第三方）；OpenAI 兼容 API 格式
**定价：** ~$0.10-0.80/分钟，取决于分辨率（估计每片段比 Sora 2 便宜 10-100 倍）

**功能：**
- 最高 2K 分辨率下最长 20 秒
- 同步音视频生成（双分支扩散 Transformer）
- 文本到视频和图像到视频
- 最多 12 个参考文件用于多模态输入
- OpenAI 兼容 API 结构

**广告创意用例：**
- 低成本大批量短视频广告制作
- 一次性生成带同步配音和音效的视频广告
- 多参考生成（输入产品图片、品牌资产、样式参考）
- 快速迭代视频广告概念

**文档：** [Seedance](https://seed.bytedance.com/en/seedance2_0)

---

### Higgsfield

具有电影感相机控制的全栈视频创作平台。

**最适合：** 社交视频广告、电影感风格、移动优先内容
**平台：** [higgsfield.ai](https://higgsfield.ai/)

**功能：**
- 50+ 种专业相机运动（缩放、平移、FPV 无人机拍摄）
- 图像到视频动画
- 内置编辑、过渡和关键帧
- 一站式工作流程：图像生成、动画、编辑

**广告创意用例：**
- 具有电影感的社交媒体视频广告
- 将产品图片动画化为动态视频
- 创建具有不同相机样式的多个视频变体
- 为社交活动快速制作视频内容

---

### 视频工具比较

| 工具 | 最大长度 | 音频 | 分辨率 | API | 最适合 |
|------|-----------|-------|------------|-----|----------|
| **Veo 3.1** | 60 sec | Native | 1080p/4K | Gemini | Vertical social video |
| **Kling 2.6** | 3 min | Native | 1080p | Third-party | Longer cinematic |
| **Runway Gen-4** | 10 sec | No | 1080p | Official | Controlled, consistent |
| **Sora 2** | 60 sec | Native | 1080p | Official | Dialogue-heavy |
| **Seedance 2.0** | 20 sec | Native | 2K | Official + third-party | Affordable high-volume |
| **Higgsfield** | Varies | Yes | 1080p | Web-based | Social, mobile-first |

---

## Voice & Audio Generation

For layering realistic voiceovers onto video ads, adding narration to product demos, or generating audio for Remotion-rendered videos. These tools turn ad scripts into natural-sounding voice tracks.

### When to Use Voice Tools

Many video generators (Veo, Kling, Sora, Seedance) now include native audio. Use standalone voice tools when you need:

- **Voiceover on silent video** — Runway Gen-4 and Remotion produce silent output
- **Brand voice consistency** — Clone a specific voice for all ads
- **Multi-language versions** — Same ad script in 20+ languages
- **Script iteration** — Re-record voiceover without reshooting video
- **Precise control** — Exact timing, emotion, and pacing

---

### ElevenLabs

The market leader in realistic voice generation and voice cloning.

**Best for:** Most natural-sounding voiceovers, brand voice cloning, multilingual
**API:** REST API with streaming support
**Pricing:** ~$0.12-0.30 per 1,000 characters depending on plan; starts at $5/month

**Capabilities:**
- 29+ languages with natural accent and intonation
- Voice cloning from short audio clips (instant) or longer recordings (professional)
- Emotion and style control
- Streaming for real-time generation
- Voice library with hundreds of pre-built voices

**Ad creative use cases:**
- Generate voiceover tracks for video ads
- Clone your brand spokesperson's voice for all ad variations
- Produce the same ad in 10+ languages from one script
- A/B test different voice styles (authoritative vs. friendly vs. urgent)

**API example:**
```bash
curl -X POST "https://api.elevenlabs.io/v1/text-to-speech/{voice_id}" \
  -H "xi-api-key: $ELEVENLABS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Stop wasting hours on manual reporting. Try DataFlow free for 14 days.",
    "model_id": "eleven_multilingual_v2",
    "voice_settings": {"stability": 0.5, "similarity_boost": 0.75}
  }' --output voiceover.mp3
```

**Docs:** [ElevenLabs API](https://elevenlabs.io/docs/api-reference/text-to-speech)

---

### OpenAI TTS

Simple, affordable text-to-speech built into the OpenAI API.

**Best for:** Quick voiceovers, cost-effective at scale, simple integration
**API:** OpenAI API (same SDK as GPT/DALL-E)
**Pricing:** $15/million chars (standard), $30/million chars (HD); ~$0.015/min with gpt-4o-mini-tts

**Capabilities:**
- 13 built-in voices (no custom cloning)
- Multiple languages
- Real-time streaming
- HD quality option
- Simple API — same SDK you already use for GPT

**Ad creative use cases:**
- Fast, cheap voiceover for draft/test ad versions
- High-volume narration at low cost
- Prototype ad audio before investing in premium voice

**Docs:** [OpenAI TTS](https://platform.openai.com/docs/guides/text-to-speech)

---

### Cartesia Sonic

Ultra-low latency voice generation built for real-time applications.

**Best for:** Real-time voice, lowest latency, emotional expressiveness
**API:** REST + WebSocket streaming
**Pricing:** Starts at $5/month; pay-as-you-go from $0.03/min

**Capabilities:**
- 40ms time-to-first-audio (fastest in class)
- 15+ languages
- Nonverbal expressiveness: laughter, breathing, emotional inflections
- Sonic Turbo for even lower latency
- Streaming API for real-time generation

**Ad creative use cases:**
- Real-time ad preview during creative iteration
- Interactive demo videos with dynamic narration
- Ads requiring natural laughter, sighs, or emotional reactions

**Docs:** [Cartesia Sonic](https://docs.cartesia.ai/build-with-cartesia/tts-models/latest)

---

### Voicebox (Open Source)

Free, local-first voice synthesis studio powered by Qwen3-TTS. The open-source alternative to ElevenLabs.

**Best for:** Free voice cloning, local/private generation, zero-cost batch production
**API:** Local REST API at `http://localhost:8000`
**Pricing:** Free (MIT license). Runs entirely on your machine.
**Stack:** Tauri (Rust) + React + FastAPI (Python)

**Capabilities:**
- Voice cloning from short audio samples via Qwen3-TTS
- Multi-language support (English, Chinese, more planned)
- Multi-track timeline editor for composing conversations
- 4-5x faster inference on Apple Silicon via MLX Metal acceleration
- Local REST API for programmatic generation
- No cloud dependency — all processing on-device

**Ad creative use cases:**
- Free voice cloning for brand spokesperson across all ad variations
- Batch generate voiceovers without per-character costs
- Private/local generation when ad content is sensitive or pre-launch
- Prototype voice variations before committing to a paid service

**API example:**
```bash
curl -X POST http://localhost:8000/generate \
  -H "Content-Type: application/json" \
  -d '{"text": "Stop wasting hours on manual reporting.", "profile_id": "abc123", "language": "en"}'
```

**Install:** Desktop apps for macOS and Windows at [voicebox.sh](https://voicebox.sh), or build from source:
```bash
git clone https://github.com/jamiepine/voicebox.git
cd voicebox && make setup && make dev
```

**Docs:** [GitHub](https://github.com/jamiepine/voicebox)

---

### Other Voice Tools

| Tool | Best For | Differentiator | API |
|------|----------|---------------|-----|
| **PlayHT** | Large voice library, low latency | 900+ voices, <300ms latency, ultra-realistic | [play.ht](https://play.ht/) |
| **Resemble AI** | Enterprise voice cloning | On-premise deployment, real-time speech-to-speech | [resemble.ai](https://www.resemble.ai/) |
| **WellSaid Labs** | Ethical, commercial-safe voices | Voices from compensated actors, safe for commercial use | [wellsaid.io](https://www.wellsaid.io/) |
| **Fish Audio** | Budget-friendly, emotion control | ~50-70% cheaper than ElevenLabs, emotion tags | [fish.audio](https://fish.audio/) |
| **Murf AI** | Non-technical teams | Browser-based studio, 200+ voices | [murf.ai](https://murf.ai/) |
| **Google Cloud TTS** | Google ecosystem, scale | 220+ voices, 40+ languages, enterprise SLAs | [Google TTS](https://cloud.google.com/text-to-speech) |
| **Amazon Polly** | AWS ecosystem, cost | Neural voices, SSML control, cheap at volume | [Amazon Polly](https://aws.amazon.com/polly/) |

---

### Voice Tool Comparison

| Tool | Quality | Cloning | Languages | Latency | Price/1K chars |
|------|---------|---------|-----------|---------|----------------|
| **ElevenLabs** | Best | Yes (instant + pro) | 29+ | ~200ms | $0.12-0.30 |
| **OpenAI TTS** | Good | No | 13+ | ~300ms | $0.015-0.030 |
| **Cartesia Sonic** | Very good | No | 15+ | ~40ms | ~$0.03/min |
| **PlayHT** | Very good | Yes | 140+ | <300ms | ~$0.10-0.20 |
| **Fish Audio** | Good | Yes | 13+ | ~200ms | ~$0.05-0.10 |
| **WellSaid** | Very good | No (actor voices) | English | ~300ms | Custom pricing |
| **Voicebox** | Good | Yes (local) | 2+ | Local | Free (open source) |

### Choosing a Voice Tool

```
Need voiceover for ads?
├── Need to clone a specific brand voice?
│   ├── Best quality → ElevenLabs
│   ├── Enterprise/on-premise → Resemble AI
│   └── Budget-friendly → Fish Audio, PlayHT
├── Need multilingual (same ad, many languages)?
│   ├── Most languages → PlayHT (140+)
│   └── Best quality → ElevenLabs (29+)
├── Need free / open source / local?
│   └── Voicebox (MIT, runs on your machine)
├── Need cheap, fast, good-enough?
│   └── OpenAI TTS ($0.015/min)
├── Need commercially-safe licensing?
│   └── WellSaid Labs (actor-compensated voices)
└── Need real-time/interactive?
    └── Cartesia Sonic (40ms TTFA)
```

### Workflow: Voice + Video

```
1. Write ad script (use ad-creative skill for copy)
2. Generate voiceover with ElevenLabs/OpenAI TTS
3. Generate or render video:
   a. Silent video from Runway/Remotion → layer voice track
   b. Or use Veo/Sora/Seedance with native audio (skip separate VO)
4. Combine with ffmpeg if layering separately:
   ffmpeg -i video.mp4 -i voiceover.mp3 -c:v copy -c:a aac output.mp4
5. Generate variations (different scripts, voices, or languages)
```

---

## Code-Based Video: Remotion

For templated, data-driven video ads at scale, Remotion is the best option. Unlike AI video generators that produce unique video from prompts, Remotion uses React code to render deterministic, brand-perfect video from templates and data.

**Best for:** Templated ad variations, personalized video, brand-consistent production
**Stack:** React + TypeScript
**Pricing:** Free for individuals/small teams; commercial license required for 4+ employees
**Docs:** [remotion.dev](https://www.remotion.dev/)

### Why Remotion for Ads

| AI Video Generators | Remotion |
|---------------------|----------|
| Unique output each time | Deterministic, pixel-perfect |
| Prompt-based, less control | Full code control over every frame |
| Hard to match brand exactly | Exact brand colors, fonts, spacing |
| One-at-a-time generation | Batch render hundreds from data |
| No dynamic data insertion | Personalize with names, prices, stats |

### Ad Creative Use Cases

**1. Dynamic product ads**
Feed a JSON array of products and render a unique video ad for each:
```tsx
// Simplified Remotion component for product ads
export const ProductAd: React.FC<{
  productName: string;
  price: string;
  imageUrl: string;
  tagline: string;
}> = ({productName, price, imageUrl, tagline}) => {
  return (
    <AbsoluteFill style={{backgroundColor: '#fff'}}>
      <Img src={imageUrl} style={{width: 400, height: 400}} />
      <h1>{productName}</h1>
      <p>{tagline}</p>
      <div className="price">{price}</div>
      <div className="cta">Shop Now</div>
    </AbsoluteFill>
  );
};
```

**2. A/B test video variations**
Render the same template with different headlines, CTAs, or color schemes:
```tsx
const variations = [
  {headline: "Save 50% Today", cta: "Get the Deal", theme: "urgent"},
  {headline: "Join 10K+ Teams", cta: "Start Free", theme: "social-proof"},
  {headline: "Built for Speed", cta: "Try It Now", theme: "benefit"},
];
// Render all variations programmatically
```

**3. Personalized outreach videos**
Generate videos addressing prospects by name for cold outreach or sales.

**4. Social ad batch production**
Render the same content across different aspect ratios:
- 1:1 for feed
- 9:16 for Stories/Reels
- 16:9 for YouTube

### Remotion Workflow for Ad Creative

```
1. Design template in React (or use AI to generate the component)
2. Define data schema (products, headlines, CTAs, images)
3. Feed data array into template
4. Batch render all variations
5. Upload to ad platform
```

### Getting Started

```bash
# Create a new Remotion project
npx create-video@latest

# Render a single video
npx remotion render src/index.ts MyComposition out/video.mp4

# Batch render from data
npx remotion render src/index.ts MyComposition --props='{"data": [...]}'
```

---

## Choosing the Right Tool

### Decision Tree

```
Need video ads?
├── Templated, data-driven (same structure, different data)
│   └── Use Remotion
├── Unique creative from prompts (exploratory)
│   ├── Need dialogue/voiceover? → Sora 2, Veo 3.1, Kling 2.6, Seedance 2.0
│   ├── Need consistency across scenes? → Runway Gen-4
│   ├── Need vertical social video? → Veo 3.1 (native 9:16)
│   ├── Need high volume at low cost? → Seedance 2.0
│   └── Need cinematic camera work? → Higgsfield, Kling
└── Both → Use AI gen for hero creative, Remotion for variations

Need image ads?
├── Need text/headlines in image? → Ideogram
├── Need product consistency across variations? → Flux (multi-ref)
├── Need quick iterations on existing images? → Nano Banana Pro
├── Need highest visual quality? → Flux Pro, Midjourney
└── Need high volume at low cost? → Flux Klein, Nano Banana
```

### Cost Comparison for 100 Ad Variations

| Approach | Tool | Approximate Cost |
|----------|------|-----------------|
| 100 static images | Nano Banana Pro | ~$4-24 |
| 100 static images | Flux Dev | ~$1-2 |
| 100 static images | Ideogram API | ~$6 |
| 100 × 15-sec videos | Veo 3.1 Fast | ~$225 |
| 100 × 15-sec videos | Remotion (templated) | ~$0 (self-hosted render) |
| 10 hero videos + 90 templated | Veo + Remotion | ~$22 + render time |

### Recommended Workflow for Scaled Ad Production

1. **Generate hero creative** with AI (Nano Banana, Flux, Veo) — high-quality, exploratory
2. **Build templates** in Remotion based on winning creative patterns
3. **Batch produce variations** with Remotion using data (products, headlines, CTAs)
4. **Iterate** — use AI tools for new angles, Remotion for scale

This hybrid approach gives you the creative exploration of AI generators and the consistency and scale of code-based rendering.

---

## Platform-Specific Image Specs

When generating images for ads, request the correct dimensions:

| Platform | Placement | Aspect Ratio | Recommended Size |
|----------|-----------|-------------|-----------------|
| Meta Feed | Single image | 1:1 | 1080x1080 |
| Meta Stories/Reels | Vertical | 9:16 | 1080x1920 |
| Meta Carousel | Square | 1:1 | 1080x1080 |
| Google Display | Landscape | 1.91:1 | 1200x628 |
| Google Display | Square | 1:1 | 1200x1200 |
| LinkedIn Feed | Landscape | 1.91:1 | 1200x627 |
| LinkedIn Feed | Square | 1:1 | 1200x1200 |
| TikTok Feed | Vertical | 9:16 | 1080x1920 |
| Twitter/X Feed | Landscape | 16:9 | 1200x675 |
| Twitter/X Card | Landscape | 1.91:1 | 800x418 |

Include these dimensions in your generation prompts to avoid needing to crop or resize.
