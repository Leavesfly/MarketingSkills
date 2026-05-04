# Marketing Skills 版本信息

所有技能的当前版本。Agent 可以通过与本地版本比对来检查更新。

| 技能 | 版本 | 最近更新 |
|-------|---------|--------------|
| ab-test-setup | 1.2.0 | 2026-03-14 |
| ad-creative | 1.2.0 | 2026-03-14 |
| ai-seo | 1.2.0 | 2026-03-14 |
| analytics-tracking | 1.2.0 | 2026-03-14 |
| aso-audit | 1.0.0 | 2026-04-21 |
| churn-prevention | 1.2.0 | 2026-03-14 |
| cold-email | 1.2.0 | 2026-03-14 |
| competitor-alternatives | 1.2.0 | 2026-03-14 |
| community-marketing | 1.0.0 | 2026-04-21 |
| competitor-profiling | 1.0.0 | 2026-04-07 |
| content-strategy | 1.2.0 | 2026-03-14 |
| copy-editing | 1.2.0 | 2026-03-14 |
| copywriting | 1.2.0 | 2026-03-14 |
| customer-research | 1.0.0 | 2026-04-21 |
| directory-submissions | 1.0.0 | 2026-04-21 |
| email-sequence | 1.2.0 | 2026-03-14 |
| form-cro | 1.2.0 | 2026-03-14 |
| free-tool-strategy | 1.2.0 | 2026-03-14 |
| launch-strategy | 1.2.0 | 2026-03-14 |
| lead-magnets | 1.0.0 | 2026-03-14 |
| marketing-ideas | 1.2.0 | 2026-03-14 |
| marketing-psychology | 1.2.0 | 2026-03-14 |
| onboarding-cro | 1.2.0 | 2026-03-14 |
| page-cro | 1.2.0 | 2026-03-14 |
| paid-ads | 1.2.0 | 2026-03-14 |
| paywall-upgrade-cro | 1.2.0 | 2026-03-14 |
| popup-cro | 1.2.0 | 2026-03-14 |
| pricing-strategy | 1.2.0 | 2026-03-14 |
| product-marketing-context | 1.2.0 | 2026-03-14 |
| programmatic-seo | 1.2.0 | 2026-03-14 |
| referral-program | 1.2.0 | 2026-03-14 |
| revops | 1.2.0 | 2026-03-14 |
| sales-enablement | 1.2.0 | 2026-03-14 |
| schema-markup | 1.2.0 | 2026-03-14 |
| seo-audit | 1.2.0 | 2026-03-14 |
| signup-flow-cro | 1.2.0 | 2026-03-14 |
| site-architecture | 1.2.0 | 2026-03-14 |
| social-content | 1.3.0 | 2026-04-24 |
| image | 1.0.0 | 2026-04-24 |
| video | 1.0.0 | 2026-04-24 |

## 近期变更

### 2026-04-24
- 新增 `image` 技能，用于 AI 图像生成、设计工具、头像/列表横幅以及优化
- 新增 `video` 技能，用于 AI 视频制作（Hyperframes、HeyGen、Veo、Runway、Kling）
- 为 `social-content`（1.3.0）新增短视频章节 —— TikTok、Reels、Shorts 框架
- 新增 HeyGen 与 Hyperframes 工具集成指南
- 修复插件市场：`source` 字段现已通过 Claude Code schema 校验（#270）
- 新增完整的 `plugin.json` 清单，包含 `"skills": "./skills"`
- 技能总数：40

### 2026-04-21
- 新增 `directory-submissions` 技能，用于 Product Hunt、G2、AI 目录与外链策略
- 新增 `competitor-profiling` 技能，用于竞品情报研究
- 为 `seo-audit`（1.2.0）新增国际化 SEO 与本地化章节
- 为 `paid-ads` 新增转化跟踪参考资料（跨平台像素配置）
- 集成 Zapier SDK，可访问 8,000+ 个应用
- 修复插件加载：从 marketplace.json 的技能路径中移除 `./` 前缀（#243）
- 强化 CLI 工具：Supermetrics API 密钥改为通过 header 传递，ZoomInfo JWT 默认屏蔽显示
- 修复 community-marketing 的 YAML frontmatter（#240）
- 修复 Zapier webhook 的 URL 校验（#247）
- 为 VERSIONS.md 补齐此前版本已发布但缺失的技能（aso-audit、community-marketing、customer-research）
- 技能总数：38

### 2026-03-14
- 新增 `lead-magnets` 技能，用于线索磁铁策略、格式选型与转化优化
- 新增 Composio 集成层，为需要 OAuth 的工具（HubSpot、Salesforce、Meta Ads、LinkedIn Ads、Google Sheets、Slack、Notion 等）提供 MCP 访问
- 新增无头 CMS 集成指南（Sanity、Contentful、Strapi），并附带 headless-cms 参考资料
- 为全部 33 个技能新增了 197 项 eval，用于自动化质量测试
- 优化全部 32 个技能的 description，提升触发短语匹配效果
- 将所有技能中僵硬的祈使句替换为基于推理的指引
- 新增 10 个 CLI 工具（airops、clay、close、coupler、crossbeam、outreach、pendo、similarweb、supermetrics、zoominfo）
- 新增 13 份集成指南
- 将现有 32 个技能从 1.1.0 → 1.2.0 版本升级

### 2026-02-27
- 将上下文路径从 `.claude/` 迁移至 `.agents/`，以实现 agent 无关的兼容性
- 所有技能现在优先检查 `.agents/product-marketing-context.md`，并将 `.claude/` 作为兼容旧环境的回退
- 更新 README 中的安装路径，使其指向 `.agents/skills/`
- 将全部 32 个技能从 1.0.0 → 1.1.0 版本升级

### 2026-02-22
- 新增 `revops` 技能，覆盖营收运营、线索生命周期、评分、路由、管道管理以及 CRM 自动化
- 新增 `sales-enablement` 技能，覆盖销售演示文稿、一页纸方案、异议处理、演示脚本以及销售行动手册

### 2026-02-21
- 新增 `site-architecture` 技能，用于网站结构规划、页面层级、导航设计、URL 结构以及内链策略

### 2026-02-18
- 新增 `ai-seo` 技能，用于 AI 搜索优化（AEO、GEO、LLMO、AI Overviews）
- 将 AEO/GEO 内容模式从 `seo-audit` 参考资料移至 `ai-seo` 技能
- 新增 `churn-prevention` 技能，覆盖取消流程、挽留方案、催缴以及付款恢复

### 2026-02-17
- 新增 `ad-creative` 技能，用于批量广告创意生成与基于效果的迭代
- 为营销平台新增 51 个零依赖 CLI 工具（`tools/clis/`）
- 新增 31 份集成指南（`tools/integrations/`）
- 新增 4 个邮件外呼 CLI：hunter、snov、lemlist、instantly
- 安全加固：meta-ads 改用 header 认证、URL 编码、输入校验
- 所有 CLI 均通过独立的 codex 审计（认证、安全、错误处理、一致性）

### 2026-01-27
- 加入初始版本跟踪
- 新增工具注册表，包含 29 份集成指南
