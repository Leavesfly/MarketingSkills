# AI 视频提示词指南

如何为 AI 视频生成模型（Veo、Runway、Kling、Pika）编写有效的提示词。

---

## 提示词结构

优秀的视频提示词遵循以下公式：

```
[主体] + [动作] + [运镜] + [视觉风格] + [光线/氛围] + [技术参数]
```

### 按使用场景的示例提示词

**产品主视觉镜头：**
```
A sleek laptop on a minimal white desk, screen glowing with a dashboard UI,
camera slowly orbits 180 degrees around the desk,
soft volumetric lighting from the left, shallow depth of field,
cinematic commercial aesthetic, 4K
```

**生活化 B-roll 空镜：**
```
A woman in a modern co-working space smiling while looking at her phone,
natural window light, candid documentary feel,
camera handheld with subtle movement, warm color grading
```

**抽象/品牌类：**
```
Flowing liquid gold particles forming the shape of a network graph,
dark background, particles catch light as they move,
slow-motion macro photography style, dramatic rim lighting
```

**SaaS 解说场景：**
```
An overhead shot of a team around a conference table pointing at charts,
camera slowly pushes in, bright modern office,
clean corporate style, even lighting, 1080p
```

---

## 运镜术语表

使用以下术语 —— 视频模型能够理解它们：

| 术语 | 效果 |
|------|--------|
| **Static** | 固定镜头，无运动 |
| **Pan left/right** | 镜头水平摇移 |
| **Tilt up/down** | 镜头垂直俯仰 |
| **Dolly in/out** | 镜头向主体推近/拉远 |
| **Orbit** | 镜头绕主体环绕 |
| **Tracking shot** | 跟拍移动中的主体 |
| **Crane/aerial** | 镜头升起或下降 |
| **Handheld** | 轻微抖动，纪录片质感 |
| **Zoom** | 镜头变焦（不同于 dolly） |
| **Slow push** | 缓慢推镜 —— 营造紧张感或聚焦 |

---

## 风格关键词

### 电影感（Cinematic）
- "cinematic color grading"
- "anamorphic lens flare"
- "shallow depth of field"
- "film grain"
- "35mm film"

### 商业/企业感
- "clean commercial lighting"
- "bright and airy"
- "professional corporate aesthetic"
- "even, diffused lighting"

### 纪录片感
- "handheld documentary style"
- "natural lighting"
- "candid, unposed"
- "observational camera"

### 社交/潮流感
- "vertical 9:16"
- "fast-paced cuts"
- "bold text overlays"
- "high contrast, saturated colors"

---

## 各模型专属建议

### Veo（Google）

- 擅长照片级写实与复杂场景
- 支持与视频同步的音频生成
- 搭配详尽、描述性强的提示词效果最佳
- 明确写出 "high resolution" 或 "1080p" 以获得最佳画质
- 能处理多个主体和场景转换

### Runway Gen-4

- 运镜控制能力强 —— 请精确指定镜头运动
- 时序一致性最佳（主体在各帧之间保持一致）
- 使用 motion brush 对特定区域做局部动效
- 图生视频表现优秀 —— 可提供参考帧
- 提示词保持在 100 词以内以获得最佳效果

### Kling

- 可生成最长 2 分钟（远超其他模型）
- 适合较长的叙事序列
- 大批量生成更具性价比
- 时长变长时画质会略有下降
- 更适合简单场景与较少主体

### Pika

- 生成速度最快（2 分钟以内）
- 适合快速迭代和尝试
- Effects 模式可为静态图片添加动效
- 最适合短片（5-15 秒）
- 对运镜的控制能力较弱

---

## 常见提示词错误

| 错误 | 为什么失败 | 修正方式 |
|---------|-------------|-----|
| "A person using our app" | 过于模糊，缺乏视觉细节 | 描述人物、场景、光线、镜头 |
| 包含文字/Logo | AI 无法渲染可读文字 | 通过 Hyperframes/CapCut 在后期叠加 |
| "Make it viral"（让它爆火） | 这不是视觉化指令 | 描述你想要的视觉风格 |
| 极长提示词（200+ 词） | 模型会失焦 | 保持 50-100 词，具体明确 |
| 不指定运镜 | 随机/固定镜头 | 始终指定运动或 "static" |
| 只写 "Realistic" | 不够具体 | "Photorealistic, natural lighting, shot on RED camera" |

---

## 提示词工作流

1. **先找参考** —— 找到一段与你想要效果接近的真实视频
2. **拆解描述** —— 分解为：主体、动作、运镜、风格、氛围
3. **生成 3-4 版变体** —— 同一概念，不同角度或风格
4. **基于最佳版本迭代** —— 根据结果细化提示词
5. **合成** —— 将 AI 素材与程序化文字/叠加元素组合

---

## 画面比例

务必在提示词或生成设置中指定：

| 平台 | 比例 | 分辨率 |
|----------|-------|-----------|
| YouTube | 16:9 | 1920x1080 或 3840x2160 |
| TikTok/Reels/Shorts | 9:16 | 1080x1920 |
| Instagram 信息流 | 1:1 或 4:5 | 1080x1080 或 1080x1350 |
| 官网头图 | 16:9 | 1920x1080 |
| LinkedIn | 16:9 或 1:1 | 1920x1080 |

---

## 成本优化

- **低分辨率迭代** —— 仅对最终版本做高清升级
- **用 Kling 做草稿** —— 每秒成本最低，终版再切换到 Veo/Runway
- **图生视频** —— 提供参考帧可节省生成点数并带来更好结果
- **批量相似提示词** —— 模型通常提供批量折扣
- **缓存并复用** —— B-roll 空镜可在多个视频中重复使用
