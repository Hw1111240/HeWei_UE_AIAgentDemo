---
name: kw-upgrade
description: 规划并执行 Knowledge Workshop consumer upgrades。
---

<!-- knowledge-workshop:generated canonical-skill source=share/knowledge_workshop/templates/agent-skills/kw-upgrade/SKILL.md.tmpl source-sha256=b891dd4526310dbbb9abc0eb0248d4ffa3da8aec575f67481d07aa3567ef5b7c -->

# Upgrade

当 consumer workspace 需要 Knowledge Workshop version update 或 entrypoint refresh 时使用本 skill。

## 流程

1. 读取 `.kw/workspace/workspace.json` 和 `.kw/kw-lock.json`。
2. 运行 `kw control update-advisory --consumer-root .` 做 read-only update check。
3. 如果其他 `kw` 命令返回 `runtime_update_decision_required`，把它当作 agent-facing 用户决策：报告 current/latest/update kind，然后更新或运行返回的 dismiss command，再重试原命令。
4. 运行 `kw control upgrade-plan --consumer-root . --to <version|latest>`。
5. 对 major upgrades，写入前创建 migration change。
6. 用 `kw control update --consumer-root . --version <version> --yes` 执行。
7. 用 `kw change validate` 和 `kw change sync` 验证。
