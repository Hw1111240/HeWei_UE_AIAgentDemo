---
name: kw-archive-change
description: 在验证完成后归档已完成的 Knowledge Workshop change。
---

<!-- knowledge-workshop:generated canonical-skill source=share/knowledge_workshop/templates/agent-skills/kw-archive-change/SKILL.md.tmpl source-sha256=73131ae22458f3641dba4cc888017448ddede0774da3462d2ab80021c641202f -->

# 归档 Change

仅对已 completed 的 change 使用本 skill。

## 流程

1. 运行 `kw change validate --change <change>`。
2. 确认 change status 是 `completed`。
3. 运行 `kw change archive-sync --change <change>`。
4. 报告 archive path 和任何 validation warnings。
