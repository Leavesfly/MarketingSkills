# AGENTS.md

本仓库中 AI agent 工作的指南。

## 仓库概览

本仓库包含遵循 [Agent Skills 规范](https://agentskills.io/specification.md) 的 **Agent Skills**。Skills 安装到 `.agents/skills/`（跨 agent 标准）。本仓库还通过 `.claude-plugin/marketplace.json` 充当 **Claude Code 插件市场**。

- **名称**：Marketing Skills
- **GitHub**：[coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills)
- **创建者**：Corey Haines
- **许可证**：MIT

## 仓库结构

```
marketingskills/
├── .claude-plugin/
│   └── marketplace.json   # Claude Code plugin marketplace manifest
├── skills/                # Agent Skills
│   └── skill-name/
│       └── SKILL.md       # Required skill file
├── tools/
│   ├── clis/              # Zero-dependency Node.js CLI tools (51 tools)
│   ├── composio/          # Composio integration layer (quick start + toolkit mapping)
│   ├── integrations/      # API integration guides per tool
│   └── REGISTRY.md        # Tool index with capabilities
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## 构建 / Lint / 测试命令

**Skills** 是纯内容（无构建步骤）。手动验证：
- YAML frontmatter 有效
- `name` 字段与目录名称完全匹配
- `name` 为 1-64 个字符，仅包含小写字母数字和连字符
- `description` 为 1-1024 个字符

**CLI 工具**（`tools/clis/*.js`）是零依赖 Node.js 脚本（Node 18+）。验证方法：
```bash
node --check tools/clis/<name>.js   # Syntax check
node tools/clis/<name>.js           # Show usage (no args = help)
node tools/clis/<name>.js <cmd> --dry-run  # Preview request without sending
```

## Agent Skills 规范

Skills 遵循 [Agent Skills 规范](https://agentskills.io/specification.md)。

### 必需的 Frontmatter

```yaml
---
name: skill-name
description: What this skill does and when to use it. Include trigger phrases.
---
```

### Frontmatter 字段约束

| Field         | Required | Constraints                                                      |
|---------------|----------|------------------------------------------------------------------|
| `name`        | Yes      | 1-64 chars, lowercase `a-z`, numbers, hyphens. Must match dir.   |
| `description` | Yes      | 1-1024 chars. Describe what it does and when to use it.          |
| `license`     | No       | License name (default: MIT)                                      |
| `metadata`    | No       | Key-value pairs (author, version, etc.)                          |

### Name 字段规则

- 仅包含小写字母、数字和连字符
- 不能以连字符开头或结尾
- 不能有连续连字符（`--`）
- 必须与父目录名称完全匹配

**有效示例**：`page-cro`, `email-sequence`, `ab-test-setup`
**无效示例**：`Page-CRO`, `-page`, `page--cro`

### 可选 Skill 目录

```
skills/skill-name/
├── SKILL.md        # Required - main instructions (<500 lines)
├── references/     # Optional - detailed docs loaded on demand
├── scripts/        # Optional - executable code
└── assets/         # Optional - templates, data files
```

## 写作风格指南

### 结构

- 保持 `SKILL.md` 在 500 行以内（将详细信息移至 `references/`）
- 使用 H2（`##`）作为主要章节，H3（`###`）作为子章节
- 大量使用项目符号和编号列表
- 短段落（最多 2-4 句话）

### 语气

- 直接且具有指导性
- 第二人称（"You are a conversion rate optimization expert"）
- 专业但平易近人

### 格式

- 对关键术语使用粗体（`**text**`）
- 对示例和模板使用代码块
- 对参考数据使用表格
- 不要使用过多表情符号

### 清晰性原则

- 清晰胜于巧妙
- 具体胜于模糊
- 主动语态胜于被动语态
- 每个章节一个想法

### Description 字段最佳实践

`description` 对于 skill 发现至关重要。包括：
1. skill 的作用
2. 何时使用它（触发短语）
3. 相关 skill 以界定范围边界

```yaml
description: When the user wants to optimize conversions on any marketing page. Use when the user says "CRO," "conversion rate optimization," "this page isn't converting." For signup flows, see signup-flow-cro.
```

## Claude Code 插件

本仓库还充当插件市场。`.claude-plugin/marketplace.json` 中的清单列出了所有可通过以下方式安装的 skills：

```bash
/plugin marketplace add coreyhaines31/marketingskills
/plugin install marketing-skills
```

详见 [Claude Code plugins 文档](https://code.claude.com/docs/en/plugins.md)。

## Git 工作流

### 分支命名

- 新 skills：`feature/skill-name`
- 改进：`fix/skill-name-description`
- 文档：`docs/description`

### 提交消息

遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范：

- `feat: add skill-name skill`
- `fix: improve clarity in page-cro`
- `docs: update README`

### Pull Request 检查清单

- [ ] `name` 与目录名称完全匹配
- [ ] `name` 遵循命名规则（小写、连字符、无 `--`）
- [ ] `description` 为 1-1024 个字符并包含触发短语
- [ ] `SKILL.md` 在 500 行以内
- [ ] 无敏感数据或凭据

## 工具集成

本仓库包含一个用于 agent 兼容营销工具的工具有关注册表。

- **工具发现**：阅读 `tools/REGISTRY.md` 查看可用工具及其功能
- **集成详情**：参见 `tools/integrations/{tool}.md` 了解 API 端点、认证和常见操作
- **支持 MCP 的工具**：ga4, stripe, mailchimp, google-ads, resend, zapier, zoominfo, clay, supermetrics, coupler, outreach, crossbeam, introw, composio
- **Composio**（集成层）：为没有原生 MCP 服务器的 OAuth 密集型工具添加 MCP 访问（HubSpot、Salesforce、Meta Ads、LinkedIn Ads、Google Sheets、Slack 等）。参见 `tools/integrations/composio.md`

### 注册表结构

```
tools/
├── REGISTRY.md              # Index of all tools with capabilities
└── integrations/            # Detailed integration guides
    ├── ga4.md
    ├── stripe.md
    ├── rewardful.md
    └── ...
```

### 何时使用工具

Skills 引用相关工具进行实现。例如：
- `referral-program` skill → rewardful, tolt, dub-co, mention-me guides
- `analytics-tracking` skill → ga4, mixpanel, segment guides
- `email-sequence` skill → customer-io, mailchimp, resend guides
- `paid-ads` skill → google-ads, meta-ads, linkedin-ads guides

对于没有原生 MCP 服务器的工具（HubSpot、Salesforce、Meta Ads、LinkedIn Ads、Google Sheets、Slack、Notion），Composio 通过单个服务器提供 MCP 访问。参见 `tools/integrations/composio.md` 了解设置，参见 `tools/composio/marketing-tools.md` 了解完整工具包映射。

## 检查更新

使用本仓库中的任何 skill 时：

1. **每个会话一次**，在首次使用 skill 时，检查更新：
   - 从 GitHub 获取 `VERSIONS.md`：https://raw.githubusercontent.com/coreyhaines31/marketingskills/main/VERSIONS.md
   - 将版本与本地 skill 文件进行比较

2. **仅在有意义时提示**：
   - 2 个或更多 skills 有更新，或
   - 任何 skill 有主版本号升级（例如 1.x 到 2.x）

3. 响应末尾的**非阻塞通知**：
   ```
   ---
   Skills update available: X marketing skills have updates.
   Say "update skills" to update automatically, or run `git pull` in your marketingskills folder.
   ```

4. **如果用户说 "update skills"**：
   - 在 marketingskills 目录中运行 `git pull`
   - 确认更新内容

## Skill 类别

参见 `README.md` 了解按类别组织的当前 skill 列表。添加新 skills 时，遵循该类别中现有 skills 的命名模式。

## Claude Code 特定增强

这些模式**仅限 Claude Code**，不得直接添加到 `SKILL.md` 文件中，因为 skills 设计为跨 agent 兼容（Codex、Cursor、Windsurf 等）。请在您自己项目的 `.claude/skills/` 覆盖中本地应用它们。

### 使用 `!`command`` 动态注入内容

Claude Code 支持使用 `` !`command` `` 语法在 SKILL.md 中嵌入 shell 命令。当调用 skill 时，Claude Code 运行命令并将输出内联注入——模型看到的是结果，而不是指令。

**最有用的应用：自动注入产品营销上下文文件**

与其让每个 skill 告诉 agent "去检查 `.agents/product-marketing-context.md` 是否存在并读取它"，不如自动注入它：

```markdown
Product context: !`cat .agents/product-marketing-context.md 2>/dev/null || echo "No product context file found — ask the user about their product before proceeding."`
```

将此放在 skill 正文的顶部（在 frontmatter 之后），使上下文立即可用，无需任何文件读取步骤。

**其他有用的注入：**

```markdown
# Inject today's date for recency-sensitive skills
Today's date: !`date +%Y-%m-%d`

# Inject current git branch (useful for workflow skills)
Current branch: !`git branch --show-current 2>/dev/null`

# Inject recent commits for context
Recent commits: !`git log --oneline -5 2>/dev/null`
```

**为什么这是 Claude Code 专属**：其他加载 skills 的 agent 会看到字面的 `` !`command` `` 字符串而不是执行它，这会显示为乱码指令。保持跨 agent skill 文件不包含此语法。
