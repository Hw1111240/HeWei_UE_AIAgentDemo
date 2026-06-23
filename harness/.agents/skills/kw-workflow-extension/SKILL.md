---
name: kw-workflow-extension
description: 规划并维护 local workflow requirements 和 gates。
---

<!-- knowledge-workshop:generated canonical-skill source=share/knowledge_workshop/templates/agent-skills/kw-workflow-extension/SKILL.md.tmpl source-sha256=509f11c69f4a8bc985004b33a801ac402c7f731d1938c90623d5071bf9d8cfe1 -->

# Workflow Extension

当项目需要 default Knowledge Workshop state machine 之外的 local workflow requirements 时使用本 skill。

## 流程

1. 读取 `.kw/policies/workflow-extension.json`。
2. 判断 requirement 是 project-local，还是应进入 shared product。若可复用 lesson 适用于多个 consumer，或已有 shared rule 没能指导行为，停止本地 policy 编辑，并把候选路由到 shared product change。
3. 优先使用 declarative requirements，而不是 custom scripts。
4. 编辑后运行 `kw change validate`。
5. 用 `kw change refresh-requirements --change <change>` 刷新 active changes。

Shared default policy changes 应通过 formal change 在 Knowledge Workshop product repo 中完成。

Knowledge writing rules 属于 `kw-knowledge-writing-policy`，不要写进 workflow extension policy。
