# Gong

收入智能平台，记录、转录和分析销售对话（电话、视频会议、电子邮件），以揭示交易洞察、辅导机会和竞争情报。

## 功能

| 集成方式 | 可用 | 说明 |
|-------------|-----------|-------|
| API | ✓ | REST API，Basic Auth 或 OAuth2 |
| MCP | - | 不可用 |
| CLI | - | 不可用 |
| SDK | - | 仅 REST API；通过 dltHub 提供社区 Python 客户端 |

## 身份验证

- **类型**：Basic Auth（Access Key + Secret）或已发布应用的 OAuth2
- **获取密钥**：仅限管理员 — Settings > API，网址 https://app.gong.io
- **基础 URL**：租户特定 — 从您的 Gong API 设置中检索（通常为 `https://{tenant}.api.gong.io/v2/`）
- **文档**：https://help.gong.io/docs/what-the-gong-api-provides

## API Endpoints

Most Gong API endpoints use **POST** with JSON request bodies for filtering. Check the [official API docs](https://gong.app.gong.io/settings/api/documentation) for current endpoint availability.

### Calls

```bash
# List calls (with date/user filters)
POST /v2/calls/extensive

# Get call transcripts (batch, by call IDs)
POST /v2/calls/transcript
```

### Users & Stats

```bash
# List users
GET /v2/users

# Get activity stats (talk ratio, questions asked, longest monologue)
POST /v2/stats/activity/day-by-day
```

### Engagement Flows

```bash
# List flows
GET /v2/flows

# Get flow analytics
GET /v2/flows/{id}/analytics
```

## Key Data Points

### Per Call
- Full transcript with speaker labels and timestamps
- Talk-to-listen ratio per participant
- Topics discussed (auto-detected)
- Questions asked (count and content)
- Longest monologue duration
- Next steps mentioned
- Competitor mentions
- Pricing discussions flagged

### Per Deal
- All associated calls and emails
- Deal stage progression
- Risk signals (gone dark, competitor mentioned, champion left)
- Engagement score

### Per Rep
- Talk ratio trends
- Question frequency
- Topic coverage vs. playbook
- Win rate correlation with behaviors

## Common Agent Operations

### Extract Competitive Intelligence from Calls

1. Query calls mentioning competitor names
2. Extract: objections raised, features compared, pricing discussed
3. Synthesize into competitive battlecard updates
4. Track competitor mention frequency over time

### Mine Calls for Customer Research

1. Pull transcripts from recent won/lost deals
2. Extract: pain points, trigger events, decision criteria, language used
3. Feed into persona building and messaging work
4. Identify recurring objections for sales enablement

### Revenue Attribution

1. Pull call data alongside CRM deal data
2. Map which content/pages were discussed in winning deals
3. Identify which talking points correlate with closed-won
4. Build content-to-revenue attribution reports

### Rep Coaching Insights

1. Compare top performer call patterns vs. team average
2. Identify: talk ratio, question frequency, topic coverage gaps
3. Surface specific call moments for coaching review
4. Track improvement over time

## Rate Limits

- 3 API calls per second
- 10,000 API calls per day
- Pagination required for large result sets

## When to Use

- Mining sales call transcripts for customer research and VOC data
- Extracting competitive intelligence from prospect conversations
- Building revenue attribution models (content → deal influence)
- Analyzing win/loss patterns across deal transcripts
- Coaching sales reps based on conversation analytics
- Identifying common objections and buying signals

## Limitations

- API access requires admin credentials
- Transcript quality depends on call audio quality
- Rate limits (10k/day) may constrain large-scale analysis
- Pricing is enterprise-level (not publicly listed, typically $100+/user/month)
- Requires team adoption — records calls via integrations, but also supports uploading calls from non-integrated telephony systems

## Relevant Skills

- customer-research
- sales-enablement
- competitor-alternatives
- revops
- cold-email

## Sources

- [Gong API overview](https://help.gong.io/docs/what-the-gong-api-provides)
- [Gong API documentation](https://gong.app.gong.io/settings/api/documentation)
- [Call upload support](https://help.gong.io/docs/uploading-calls-from-a-non-integrated-telephony-system)
