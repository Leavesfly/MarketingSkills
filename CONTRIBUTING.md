# 贡献指南

感谢你有兴趣为 Marketing Skills 做贡献！本指南将帮助你新增技能或改进现有技能。

## 申请新技能

你也可以通过[提交技能申请](https://github.com/coreyhaines31/marketingskills/issues/new?template=skill-request.yml)来建议新的技能。

## 新增技能

### 1. 创建技能目录

```bash
mkdir -p skills/your-skill-name
```

### 2. 创建 SKILL.md 文件

每个技能都需要一个带有 YAML frontmatter 的 `SKILL.md` 文件：

```yaml
---
name: your-skill-name
description: When to use this skill. Include trigger phrases and keywords that help agents identify relevant tasks.
---

# Your Skill Name

Instructions for the agent go here...
```

可选的 frontmatter 字段：`license`（默认：MIT）、`metadata`（作者、版本等）

### 3. 遵循命名规范

- **目录名**：小写字母，仅使用连字符（例如 `email-sequence`）
- **name 字段**：必须与目录名完全一致
- **description**：1-1024 个字符，需包含触发短语

### 4. 组织技能结构

```
skills/your-skill-name/
├── SKILL.md           # 必需 - 主要说明
├── references/        # 可选 - 附加文档
│   └── guide.md
├── scripts/           # 可选 - 可执行代码
│   └── helper.py
└── assets/            # 可选 - 模板、图片、数据
    └── template.json
```

### 5. 编写高效的说明

- 保持 `SKILL.md` 不超过 500 行
- 将详细的参考资料移至 `references/`
- 提供分步说明
- 添加输入和输出的示例
- 覆盖常见的边界情况

## 改进现有技能

1. 完整阅读现有技能
2. 在本地测试你的变更
3. 保持变更聚焦且精简
4. 如果进行了重大变更，更新 metadata 中的版本号

## 提交你的贡献

1. Fork 本仓库
2. 创建一个功能分支（`git checkout -b feature/new-skill-name`）
3. 完成你的变更
4. 在本地使用 AI agent 进行测试
5. 使用合适的模板提交 PR：
   - [新技能](?template=new-skill.md)
   - [技能更新](?template=skill-update.md)
   - [文档](?template=documentation.md)

## 技能质量检查清单

- [ ] `name` 与目录名一致
- [ ] `description` 清晰说明了何时使用该技能
- [ ] 说明清晰且可操作
- [ ] 不含敏感数据或凭证
- [ ] 遵循仓库中既有技能的模式

## 有问题？

如有疑问或需要对贡献进行协助，请提交一个 issue。
