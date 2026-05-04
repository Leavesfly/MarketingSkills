# 竞争对手页面的内容架构

如何构建和维护可扩展比较页面的竞争对手数据。

## 目录
- 集中式竞争对手数据
- 竞争对手数据模板
- 您的产品数据
- 页面生成
- 索引页面结构（替代品索引、vs 比较索引、索引页面最佳实践）
- 页脚导航

## 集中式竞争对手数据

为每个竞争对手创建单一事实来源：

```
competitor_data/
├── notion.md
├── airtable.md
├── monday.md
└── ...
```

---

## 竞争对手数据模板

每个竞争对手，记录：

```yaml
name: Notion
website: notion.so
tagline: "The all-in-one workspace"
founded: 2016
headquarters: San Francisco

# 定位
primary_use_case: "docs + light databases"
target_audience: "teams wanting flexible workspace"
market_position: "premium, feature-rich"

# 定价
pricing_model: per-seat
free_tier: true
free_tier_limits: "limited blocks, 1 user"
starter_price: $8/user/month
business_price: $15/user/month
enterprise: custom

# 功能（评分 1-5 或描述）
features:
  documents: 5
  databases: 4
  project_management: 3
  collaboration: 4
  integrations: 3
  mobile_app: 3
  offline_mode: 2
  api: 4

# 优势（诚实）
strengths:
  - Extremely flexible and customizable
  - Beautiful, modern interface
  - Strong template ecosystem
  - Active community

# 劣势（公平）
weaknesses:
  - Can be slow with large databases
  - Learning curve for advanced features
  - Limited automations compared to dedicated tools
  - Offline mode is limited

# 最适合
best_for:
  - Teams wanting all-in-one workspace
  - Content-heavy workflows
  - Documentation-first teams
  - Startups and small teams

# 不太理想
not_ideal_for:
  - Complex project management needs
  - Large databases (1000s of rows)
  - Teams needing robust offline
  - Enterprise with strict compliance

# 常见投诉（来自评论）
common_complaints:
  - "Gets slow with lots of content"
  - "Hard to find things as workspace grows"
  - "Mobile app is clunky"

# 迁移说明
migration_from:
  difficulty: medium
  data_export: "Markdown, CSV, HTML"
  what_transfers: "Pages, databases"
  what_doesnt: "Automations, integrations setup"
  time_estimate: "1-3 days for small team"
```

---

## 您的产品数据

为您自己使用相同的结构——要诚实：

```yaml
name: [Your Product]
# ... same fields

strengths:
  - [Your real strengths]

weaknesses:
  - [Your honest weaknesses]

best_for:
  - [Your ideal customers]

not_ideal_for:
  - [Who should use something else]
```

---

## 页面生成

每个页面从集中式数据中提取：

- **[Competitor] Alternative 页面**：提取竞争对手数据 + 您的数据
- **[Competitor] Alternatives 页面**：提取竞争对手数据 + 您的数据 + 其他替代品
- **You vs [Competitor] 页面**：提取您的数据 + 竞争对手数据
- **[A] vs [B] 页面**：提取两个竞争对手数据 + 您的数据

**好处**：
- 更新一次竞争对手定价，所有地方都会更新
- 添加一次新功能比较，出现在所有页面上
- 跨页面保持一致的准确性
- 更容易大规模维护

---

## 索引页面结构

### 替代品索引

**URL**：`/alternatives` 或 `/alternatives/index`

**目的**：列出所有"[Competitor] Alternative"页面

**页面结构**：
1. 标题："[Your Product] 作为替代品"
2. 简要介绍人们为什么切换到您
3. 所有替代品页面列表，包括：
   - 竞争对手名称/logo
   - 与该竞争对手的关键差异化因素的一行摘要
   - 链接到完整比较
4. 人们切换的常见原因（汇总）
5. 行动号召

**示例**：
```markdown
## 探索 [Your Product] 作为替代品

想要切换？看看 [Your Product] 与您正在评估的工具相比如何：

- **[Notion Alternative](/alternatives/notion)** — 更适合需要 [X] 的团队
- **[Airtable Alternative](/alternatives/airtable)** — 更适合需要 [Y] 的团队
- **[Monday Alternative](/alternatives/monday)** — 更适合需要 [Z] 的团队
```

---

### Vs 比较索引

**URL**：`/vs` 或 `/compare`

**目的**：列出所有"You vs [Competitor]"和"[A] vs [B]"页面

**页面结构**：
1. 标题："比较 [Your Product]"
2. 部分："[Your Product] vs 竞争对手" — 直接比较列表
3. 部分："正面比较" — [A] vs [B] 页面列表
4. 简要方法说明
5. 行动号召

---

### 索引页面最佳实践

**保持更新**：当您添加新的比较页面时，将其添加到相关索引中。

**内部链接**：
- 从索引链接到各个页面
- 从各个页面链接回索引
- 在相关比较之间交叉链接

**SEO 价值**：
- 索引页面可以排名广泛术语，如"项目管理工具比较"
- 将链接权重传递给各个比较页面
- 帮助搜索引擎发现所有比较内容

**排序选项**：
- 按受欢迎程度（搜索量）
- 按字母顺序
- 按类别/用例
- 按添加日期（显示新鲜度）

**在索引页面上包括**：
- 最后更新日期以增加可信度
- 可用页面/比较的数量
- 如果您有很多比较，提供快速过滤器

---

## 页脚导航

网站页脚出现在所有营销页面上，使其成为竞争对手页面的强大内部链接机会。

### 选项 1：链接到索引页面（最低要求）

至少，在页脚中添加指向您的比较索引页面的链接：

```
Footer
├── Compare
│   ├── Alternatives →  /alternatives
│   └── Comparisons →  /vs
```

这确保每个营销页面都将链接权重传递给您的比较内容中心。

### 选项 2：按格式划分的页脚列（推荐用于 SEO）

为了更强的内部链接，为每种您已构建页面的格式创建专用的页脚列，直接链接到您的顶级竞争对手：

```
Footer
├── [Product] vs               ├── Alternatives to            ├── Compare
│   ├── vs Notion              │   ├── Notion Alternative     │   ├── Notion vs Airtable
│   ├── vs Airtable            │   ├── Airtable Alternative   │   ├── Monday vs Asana
│   ├── vs Monday              │   ├── Monday Alternative     │   ├── Notion vs Monday
│   ├── vs Asana               │   ├── Asana Alternative      │   ├── ...
│   ├── vs Clickup             │   ├── Clickup Alternative    │   └── View all →
│   ├── ...                    │   ├── ...                    │
│   └── View all →             │   └── View all →             │
```

**指南**：
- 每列最多包含 8 个链接（按搜索量排名的顶级竞争对手）
- 添加"查看全部"链接到完整索引页面
- 仅为您实际构建了页面的格式创建列
- 优先考虑搜索量最高的竞争对手

### 为什么页脚链接很重要

1. **全站分发**：页脚链接出现在每个营销页面上，将整个网站的链接权重传递给比较内容
2. **爬取效率**：搜索引擎快速发现所有比较页面
3. **用户发现**：评估您产品的访客可以轻松找到比较
4. **竞争定位**：向搜索引擎表明您是该领域的关键参与者

### 实施说明

- 添加新的高优先级比较页面时更新页脚
- 保持页脚简洁——不要列出每个比较，只列出顶级的
- 使列标题与您的 URL 结构匹配（例如，"vs"列 → `/vs/` URLs）
- 考虑移动端：列可能会堆叠，因此按优先级排序
