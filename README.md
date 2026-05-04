# 面向 AI Agent 的 Marketing Skills（营销技能）

一套聚焦于营销任务的 AI Agent（AI 智能体）技能合集。为那些希望借助 AI 编码智能体完成 CRO（转化率优化）、文案撰写、SEO（搜索引擎优化）、analytics（数据分析）与 growth engineering（增长工程）工作的技术型营销人与创始人而构建。兼容 Claude Code、OpenAI Codex、Cursor、Windsurf，以及任何支持 [Agent Skills 规范](https://agentskills.io) 的智能体。

由 [Corey Haines](https://corey.co?ref=marketingskills) 构建。需要实战协助？可以了解 [Conversion Factory](https://conversionfactory.co?ref=marketingskills)——Corey 的代理公司，提供转化率优化、landing page（着陆页）与增长策略服务。想深入学习营销？订阅 [Swipe Files](https://swipefiles.com?ref=marketingskills)。想要一个使用这些 skills 的自主 AI Agent 作为你的 CMO（首席营销官）？试试 [Magister](https://magistermarketing.com?ref=marketingskills)。

刚开始接触终端和 coding agents？可以参考配套指南 [Coding for Marketers](https://codingformarketers.com?ref=marketingskills)。

**欢迎贡献！** 发现了改进某个 skill 的方式，或者有新的 skill 想要添加？[提交 PR](#contributing)。

遇到问题或有疑问？[提交 Issue](https://github.com/coreyhaines31/marketingskills/issues)——我们乐意提供帮助。

## 什么是 Skills？

Skills 是一种 Markdown 文件，用于向 AI Agent 提供针对特定任务的专业知识与工作流。当你把这些文件添加到项目中时，你的 Agent 就能识别出你正在处理营销任务，并应用合适的框架与最佳实践。

## Skills 之间如何协同

Skills 会彼此引用，并基于共享上下文之上构建。`product-marketing-context` skill 是整个体系的基础——其他每一个 skill 在执行任何操作前，都会先检查它，以便了解你的产品、受众与定位。

```
                            ┌──────────────────────────────────────┐
                            │      product-marketing-context       │
                            │    (read by all other skills first)  │
                            └──────────────────┬───────────────────┘
                                               │
    ┌──────────────┬─────────────┬─────────────┼─────────────┬──────────────┬──────────────┐
    ▼              ▼             ▼             ▼             ▼              ▼              ▼
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐ ┌──────────┐ ┌─────────────┐ ┌───────────┐
│  SEO &   │ │   CRO    │ │Content & │ │  Paid &    │ │ Growth & │ │  Sales &    │ │ Strategy  │
│ Content  │ │          │ │   Copy   │ │Measurement │ │Retention │ │    GTM      │ │           │
├──────────┤ ├──────────┤ ├──────────┤ ├────────────┤ ├──────────┤ ├─────────────┤ ├───────────┤
│seo-audit │ │page-cro  │ │copywritng│ │paid-ads    │ │referral  │ │revops       │ │mktg-ideas │
│ai-seo    │ │signup-cro│ │copy-edit │ │ad-creative │ │free-tool │ │sales-enable │ │mktg-psych │
│site-arch │ │onboard   │ │cold-email│ │ab-test     │ │churn-    │ │launch       │ │customer-  │
│programm  │ │form-cro  │ │email-seq │ │analytics   │ │ prevent  │ │pricing      │ │ research  │
│schema    │ │popup-cro │ │social    │ │            │ │community │ │comp-alts    │ │           │
│content   │ │paywall   │ │video     │ │            │ │lead-magnt│ │comp-profile │ │           │
│aso-audit │ │          │ │image     │ │            │ │          │ │directory    │ │           │
└────┬─────┘ └────┬─────┘ └────┬─────┘ └─────┬──────┘ └────┬─────┘ └──────┬──────┘ └─────┬─────┘
     │            │            │              │             │              │              │
     └────────────┴─────┬──────┴──────────────┴─────────────┴──────────────┴──────────────┘
                        │
         Skills cross-reference each other:
           copywriting ↔ page-cro ↔ ab-test-setup
           revops ↔ sales-enablement ↔ cold-email
           seo-audit ↔ schema-markup ↔ ai-seo
           customer-research → copywriting, page-cro, competitor-alternatives
```

完整的依赖关系图请参见每个 skill 的 **Related Skills（相关 Skills）** 章节。

## 可用的 Skills 列表

<!-- SKILLS:START -->
| Skill | Description |
|-------|-------------|
| [ab-test-setup](skills/ab-test-setup/) | 当用户想要规划、设计或实施 A/B 测试或实验，或构建增长实验计划时使用。也适用于用户提到"A/B... |
| [ad-creative](skills/ad-creative/) | 当用户想要为任何付费广告平台生成、迭代或扩展广告创意——标题、描述、主要文本或完整广告变体时使用。也适用于用户提到“广告文案变体”、“广告创意”、“生成标题”、“RSA... |
| [ai-seo](skills/ai-seo/) | 当用户想要优化内容以在 AI 搜索引擎中被发现、被 LLM 引用或出现在 AI 生成的答案中时使用。也适用于用户提到'AI SEO'、'AEO'、'GEO'、'LLMO'、'答案引擎优化'、'生成式引擎优化'、'LLM 优化'、'AI... |
| [analytics-tracking](skills/analytics-tracking/) | 当用户想要设置、改进或审计分析跟踪和度量时使用。也适用于用户提到"设置跟踪"、"GA4"、"Google Analytics"、"转化跟踪"、"事件跟踪"、"UTM... |
| [aso-audit](skills/aso-audit/) | 当用户想要审计或优化 App Store 或 Google Play 应用商店列表时使用。也适用于用户提到"ASO... |
| [churn-prevention](skills/churn-prevention/) | 当用户想要减少流失、构建取消流程、设置挽留优惠、恢复失败付款或实施留存策略时使用。也适用于用户提到'流失'、'取消流程'、'离站'、'挽留优惠'、'催款'、'失败付款恢复'、'赢回'、'留存'、'退出调查'、'暂停订阅'、'非自愿流失'、... |
| [cold-email](skills/cold-email/) | 撰写能获得回复的 B2B 冷邮件和跟进序列。当用户想要撰写冷 Outreach 邮件、潜在客户开发邮件、冷邮件活动、销售开发邮件或 SDR 邮件时使用。当用户提到"冷... |
| [community-marketing](skills/community-marketing/) | 构建并利用在线社区来推动产品增长和品牌忠诚度。当用户想要创建社区策略、发展 Discord 或 Slack 社区、管理论坛或... |
| [competitor-alternatives](skills/competitor-alternatives/) | 当用户想要创建竞争对手比较或替代页面以用于 SEO 和销售赋能时使用。也适用于当用户提到"alternative page"、"vs page"、"competitor comparison"、"comparison... |
| [competitor-profiling](skills/competitor-profiling/) | 当用户想要从 URL 研究、分析或剖析竞争对手时使用。也适用于当用户提到"competitor profile"、"competitor research"、"competitor analysis"、"profile this... |
| [content-strategy](skills/content-strategy/) | 当用户想要规划内容策略、决定创建什么内容或确定要涵盖哪些主题时使用。也适用于用户提到"内容策略"、"我应该写什么"、"内容创意"、"博客策略"、"主题集群"、"内容规划"、"编辑日历"、"内容营销"、"内容路线图"、"我应该创建什么内容"... |
| [copy-editing](skills/copy-editing/) | 当用户想要编辑、审查或改进现有营销文案，或刷新过时内容时使用。也适用于用户提到"编辑此文案"、"审查我的文案"、"文案反馈"、"校对"、"润色这个"、"让它更好"、"文案扫描"、"精简这个"、"这读起来很别扭"、"清理这段文本"、"太啰嗦... |
| [copywriting](skills/copywriting/) | 当用户想要为任何页面撰写、重写或改进营销文案时使用——包括首页、落地页、定价页、功能页、关于我们页面或产品页面。也用于用户说"写文案"、"改进这个文案"、"重写这个页面"、"营销文案"、"标题帮助"、"CTA... |
| [customer-research](skills/customer-research/) | 当用户想要进行、分析或综合客户研究时使用。用于用户提到"客户研究"、"ICP... |
| [directory-submissions](skills/directory-submissions/) | 当用户希望将产品提交到初创公司、SaaS、AI、Agent、MCP、无代码或评论目录以获取反向链接、域名评级和曝光时使用。当用户提到"目录提交"、"提交到目录"、"来自目录的反向链接"、"列出我的产品"、"提交到 Product... |
| [email-sequence](skills/email-sequence/) | 当用户想要创建或优化邮件序列、滴灌营销、自动化邮件流程或生命周期邮件计划时使用。也适用于用户提到"邮件序列"、"滴灌营销"、"培育序列"、"入职邮件"、"欢迎序列"、"重新互动邮件"、"邮件自动化"、"生命周期邮件"、"触发式邮件"、"邮... |
| [form-cro](skills/form-cro/) | 当用户想要优化任何非注册/登录的表单时——包括潜在客户捕获表单、联系表单、演示请求表单、申请表单、调查表单或结账表单。也适用于用户提到"表单优化"、"潜在客户表单转化"、"表单摩擦"、"表单项"、"表单完成率"、"联系表单"、"没人填写我... |
| [free-tool-strategy](skills/free-tool-strategy/) | 当用户想要规划、评估或构建用于营销目的的免费工具时 — 用于潜在客户生成、SEO... |
| [image](skills/image/) | 当用户想要为营销创建、生成、编辑或优化图像时 — 博客头图、社交图形、产品样机、个人资料横幅、列表视觉素材或品牌资产。当用户提到"AI... |
| [launch-strategy](skills/launch-strategy/) | 当用户想要规划产品发布、功能公告或发布策略时使用。也适用于用户提到"发布"、"Product Hunt"、"功能发布"、"公告"、"上市策略"、"beta... |
| [lead-magnets](skills/lead-magnets/) | 当用户想要创建、规划或优化用于电子邮件捕获或潜在客户生成的潜在客户磁铁时使用。也适用于用户提到"潜在客户磁铁"、"付费内容"、"内容升级"、"可下载内容"、"电子书"、"速查表"、"清单"、"模板下载"、"选择加入"、"免费赠品"、"PD... |
| [marketing-ideas](skills/marketing-ideas/) | 当用户需要为其 SaaS... |
| [marketing-psychology](skills/marketing-psychology/) | 当用户希望将心理学原理、思维模型或行为科学应用于营销时使用。也适用于用户提到"心理学"、"思维模型"、"认知偏差"、"说服"、"行为科学"、"人们为何购买"、"决策"、"消费者行为"、"锚定"、"社会认同"、"稀缺性"、"损失厌恶"、"框... |
| [onboarding-cro](skills/onboarding-cro/) | 当用户希望优化注册后的入职流程、用户激活、首次运行体验或价值实现时间时使用。也适用于用户提到"入职流程"、"激活率"、"用户激活"、"首次运行体验"、"空状态"、"入职清单"、"啊哈时刻"、"新用户体验"、"用户未激活"、"无人完成设置"... |
| [page-cro](skills/page-cro/) | 当用户想要优化、改进或提升任何营销页面的转化率时使用——包括首页、落地页、定价页、功能页或博客文章。也适用于用户说"CRO"、"转化率优化"、"这个页面转化不好"、"提升转化"、"为什么这个页面不起作用"、"我的落地页很糟糕"、"没人转化... |
| [paid-ads](skills/paid-ads/) | 当用户需要帮助在 Google Ads、Meta（Facebook/Instagram）、LinkedIn、Twitter/X... |
| [paywall-upgrade-cro](skills/paywall-upgrade-cro/) | 当用户想要创建或优化应用内付费墙、升级页面、追加销售弹窗或功能门时使用。也适用于用户提到"付费墙"、"升级页面"、"升级弹窗"、"追加销售"、"功能门"、"免费转付费"、"免费增值转化"、"试用到期页面"、"达到限制页面"、"套餐升级提示... |
| [popup-cro](skills/popup-cro/) | 当用户想要创建或优化弹窗、模态框、覆盖层、滑入式窗口或横幅以提升转化率时使用。也适用于用户提及"退出意图"、"弹窗转化"、"模态框优化"、"线索捕获弹窗"、"邮件收集弹窗"、"公告横幅"、"覆盖层"、"用弹窗收集邮箱"、"退出弹窗"、"滚... |
| [pricing-strategy](skills/pricing-strategy/) | 当用户需要帮助制定定价决策、包装策略或货币化策略时使用。也适用于用户提及"定价"、"定价层级"、"免费增值"、"免费试用"、"包装"、"涨价"、"价值指标"、"Van... |
| [product-marketing-context](skills/product-marketing-context/) | 当用户想要创建或更新其产品营销上下文文档时使用。也适用于用户提及"产品上下文"、"营销上下文"、"设置上下文"、"定位"、"谁是我的目标受众"、"描述我的产品"、"ICP"、"理想客户画像"，或希望避免在营销任务中重复基础信息的情况。在任... |
| [programmatic-seo](skills/programmatic-seo/) | 当用户想要使用模板和数据大规模创建 SEO 驱动的页面时使用。也适用于用户提及"程序化 SEO"、"模板页面"、"规模化页面"、"目录页面"、"位置页面"、"[关键词] + [城市] 页面"、"比较页面"、"集成页面"、"为 SEO... |
| [referral-program](skills/referral-program/) | 当用户想要创建、优化或分析推荐计划、联盟计划或口碑营销策略时使用。当用户提到"推荐"、"联盟"、"大使"、"口碑"、"病毒式循环"、"推荐好友"、"合作伙伴计划"、"推荐激励"、"如何获得推荐"、"客户推荐客户"或"联盟佣金"时也使用。每... |
| [revops](skills/revops/) | 当用户需要帮助处理收入运营、潜在客户生命周期管理或营销到销售的交接流程时使用。当用户提到"RevOps"、"收入运营"、"潜在客户评分"、"潜在客户路由"、"MQL"、"SQL"、"管道阶段"、"交易台"、"CRM... |
| [sales-enablement](skills/sales-enablement/) | 当用户想要创建销售辅助材料、推销演示文稿、单页文档、异议处理文档或演示脚本时使用。也适用于用户提到 'sales deck'、'pitch deck'、'one-pager'、'leave-behind'、'objection... |
| [schema-markup](skills/schema-markup/) | 当用户想要在其网站上添加、修复或优化 schema 标记和结构化数据时使用。也用于当用户提到"schema markup"、"structured data"、"JSON-LD"、"rich... |
| [seo-audit](skills/seo-audit/) | 当用户想要审计、审查或诊断其网站上的 SEO 问题时使用。也用于当用户提到"SEO audit"、"technical SEO"、"why am I not ranking"、"SEO issues"、"on-page... |
| [signup-flow-cro](skills/signup-flow-cro/) | 当用户想要优化注册、账户创建或试用激活流程时使用。也适用于用户提到"注册转化率"、"注册摩擦"、"注册表单优化"、"免费试用注册"、"减少注册流失"、"账户创建流程"、"没人注册"、"注册放弃"、"试用转化率"、"没人完成注册"、"注册步... |
| [site-architecture](skills/site-architecture/) | 当用户想要规划、映射或重构网站的页面层次结构、导航、URL 结构或内部链接时使用。也适用于用户提到"站点地图"、"sitemap"、"可视化站点地图"、"网站结构"、"页面层次"、"信息架构"、"IA"、"导航设计"、"URL... |
| [social-content](skills/social-content/) | 当用户需要帮助创建、安排或优化 LinkedIn、Twitter/X、Instagram、TikTok、Facebook 或其他平台的社交媒体内容时使用。当用户提到"LinkedIn 帖子"、"Twitter... |
| [video](skills/video/) | When the user wants to create, generate, or produce video content using AI tools or programmatic frameworks. Also use... |
<!-- SKILLS:END -->

## 安装方式

### 方式 1：CLI 安装（推荐）

使用 [npx skills](https://github.com/vercel-labs/skills) 直接安装 skills：

```bash
# 安装全部 skills
npx skills add coreyhaines31/marketingskills

# 安装指定的 skills
npx skills add coreyhaines31/marketingskills --skill page-cro copywriting

# 列出可用的 skills
npx skills add coreyhaines31/marketingskills --list
```

该命令会自动安装到你的 `.agents/skills/` 目录（并为 Claude Code 兼容性软链到 `.claude/skills/`）。

### 方式 2：Claude Code 插件

通过 Claude Code 内置的插件系统安装：

```bash
# 添加 marketplace
/plugin marketplace add coreyhaines31/marketingskills

# 安装全部 marketing skills
/plugin install marketing-skills
```

### 方式 3：克隆并复制

克隆整个仓库，然后复制 skills 文件夹：

```bash
git clone https://github.com/coreyhaines31/marketingskills.git
cp -r marketingskills/skills/* .agents/skills/
```

### 方式 4：Git Submodule（子模块）

作为子模块添加，便于后续更新：

```bash
git submodule add https://github.com/coreyhaines31/marketingskills.git .agents/marketingskills
```

然后从 `.agents/marketingskills/skills/` 引用相应 skills。

### 方式 5：Fork 并定制

1. Fork 本仓库
2. 根据自己的需要定制 skills
3. 将你的 fork 克隆到你的项目中

### 方式 6：SkillKit（多 Agent 支持）

使用 [SkillKit](https://github.com/rohitg00/skillkit) 在多个 AI Agent（Claude Code、Cursor、Copilot 等）上安装 skills：

```bash
# 安装全部 skills
npx skillkit install coreyhaines31/marketingskills

# 安装指定的 skills
npx skillkit install coreyhaines31/marketingskills --skill page-cro copywriting

# 列出可用的 skills
npx skillkit install coreyhaines31/marketingskills --list
```

## 从 v1.0 升级

Skills 现在使用 `.agents/` 而不是 `.claude/` 来存放 product marketing context（产品营销上下文）文件。请迁移你已有的上下文文件：

```bash
mkdir -p .agents
mv .claude/product-marketing-context.md .agents/product-marketing-context.md
```

Skills 仍会把 `.claude/` 作为回退路径检查，所以即使你没有迁移，也不会出问题。

## 使用方式

安装完成后，直接让你的 Agent 协助处理营销任务即可：

```
"Help me optimize this landing page for conversions"
→ 使用 page-cro skill

"Write homepage copy for my SaaS"
→ 使用 copywriting skill

"Set up GA4 tracking for signups"
→ 使用 analytics-tracking skill

"Create a 5-email welcome sequence"
→ 使用 email-sequence skill
```

你也可以直接调用 skills：

```
/page-cro
/email-sequence
/seo-audit
```

## Skill 分类

### 转化率优化（CRO）
- `page-cro` - 任意营销页面
- `signup-flow-cro` - 注册流程
- `onboarding-cro` - 注册后的激活
- `form-cro` - 线索捕获表单
- `popup-cro` - 模态框与覆盖层
- `paywall-upgrade-cro` - 应用内升级节点

### 内容与文案
- `copywriting` - 营销页面文案
- `copy-editing` - 已有文案的编辑与打磨
- `cold-email` - B2B 冷启动邮件与序列
- `email-sequence` - 自动化邮件流程
- `social-content` - 社交媒体内容
- `image` - AI 图像生成、设计工具与优化

### SEO 与可发现性
- `seo-audit` - 技术与页面 SEO
- `ai-seo` - AI 搜索优化（AEO、GEO、LLMO）
- `programmatic-seo` - 规模化页面生成
- `site-architecture` - 页面层级、导航、URL 结构
- `competitor-alternatives` - 对比与替代方案页面
- `schema-markup` - 结构化数据

### 付费投放与分发
- `paid-ads` - Google、Meta、LinkedIn 广告投放
- `ad-creative` - 批量广告创意生成与迭代
- `social-content` - 社交媒体排期与策略

### 衡量与实验
- `analytics-tracking` - 事件埋点搭建
- `ab-test-setup` - 实验设计

### 留存
- `churn-prevention` - 取消流程、挽留优惠、dunning（催收）、支付恢复

### 增长工程
- `free-tool-strategy` - 营销工具与计算器
- `referral-program` - 推荐与联盟计划

### 策略与变现
- `marketing-ideas` - 140 个 SaaS 营销创意
- `marketing-psychology` - 心智模型与心理学
- `launch-strategy` - 产品发布与预告
- `pricing-strategy` - 定价、打包与变现

### 销售与 RevOps（收入运营）
- `revops` - 线索生命周期、评分、路由、管线管理
- `sales-enablement` - 销售演示文稿、单页资料、异议处理文档、demo 脚本

## 贡献

发现了改进某个 skill 的方式？有新的 skill 想要建议？欢迎提交 PR 和 Issue！

新增或改进 skills 的规范请参见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可证

[MIT](LICENSE) - 你可以以任何方式自由使用这些内容。
