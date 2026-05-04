# HeyGen

AI 数字人视频生成平台。通过文本脚本创建具有逼真唇形同步、表情和手势的说话头像视频。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | Yes | REST API v2，用于视频生成、数字人、模板 |
| MCP | Yes | 官方托管 MCP 服务器 — 无需本地安装 |
| CLI | - | - |
| SDK | Yes | 提供 Node.js SDK |

## 身份验证

- **类型**：API Key
- **请求头**：`X-Api-Key: {api_key}`
- **获取密钥**：HeyGen 仪表板中的 Settings > API

## MCP 服务器设置

HeyGen 提供托管的远程 MCP 服务器。无需本地安装。

### Claude Code / Claude Desktop

添加到你的 MCP 配置中：

```json
{
  "mcpServers": {
    "heygen": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.heygen.com/mcp"]
    }
  }
}
```

首次使用时，通过浏览器 OAuth 进行身份验证。MCP 服务器公开以下工具：
- 从脚本创建视频
- 列出和选择数字人
- 管理模板
- 检查视频状态

## API 快速入门

### 创建视频

```bash
curl -X POST https://api.heygen.com/v2/video/generate \
  -H "X-Api-Key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "video_inputs": [{
      "character": {
        "type": "avatar",
        "avatar_id": "AVATAR_ID",
        "avatar_style": "normal"
      },
      "voice": {
        "type": "text",
        "input_text": "Your script goes here.",
        "voice_id": "VOICE_ID"
      }
    }],
    "dimension": {
      "width": 1920,
      "height": 1080
    }
  }'
```

### 列出数字人

```bash
curl https://api.heygen.com/v2/avatars \
  -H "X-Api-Key: YOUR_API_KEY"
```

### 检查视频状态

```bash
curl https://api.heygen.com/v1/video_status.get?video_id=VIDEO_ID \
  -H "X-Api-Key: YOUR_API_KEY"
```

## 常见营销用例

| 用例 | 方法 |
|----------|----------|
| 产品讲解 | 从功能编写脚本 → 数字人演示 |
| 功能公告 | 使用数字人 + 屏幕录制的模板 |
| 多语言内容 | 相同脚本，不同语言/声音 |
| 个性化外展 | 脚本中使用动态变量（姓名、公司） |
| 每周更新 | 重复使用模板，替换脚本文本 |

## 自定义数字人

上传一段 2-5 分钟的你自己的说话视频以创建数字分身：
- 外观和声音与你相似
- 从文本脚本生成无限视频
- 适用于 Creator 计划及更高版本

## 定价

| 计划 | 视频/月 | 最大时长 |
|------|-----------|-------------|
| Free | 3 | 3 分钟 |
| Creator | 无限制 | 5 分钟 |
| Business | 无限制 | 20 分钟 |
| Enterprise | 无限制 | 自定义 |

查看 [heygen.com/pricing](https://www.heygen.com/pricing) 获取当前价格 — 价格经常变动。

## 速率限制

- 免费版：每月 3 个视频
- 付费版：基于计划层级，有并发生成限制
- API 速率限制：检查响应头中的 `X-RateLimit-*`

## 相关技能

- video
- social-content
- ad-creative
- sales-enablement
