---
name: kw-capability-package
description: 创建、验证、打包、发布并安装验证 reusable capability packages。
---

<!-- knowledge-workshop:generated canonical-skill source=share/knowledge_workshop/templates/agent-skills/kw-capability-package/SKILL.md.tmpl source-sha256=8fdf6b2ebea43950f240371bc58d730ea97f74c43f10d20f8ddd8d8ec3976bea -->

# Capability Package

当能力已有或需要 `capability-package.json`，并且要被其他 consumer install、lock 或 reuse 时使用本 skill。

不要把本 skill 用于 local-only project activation。如果没有 `capability-package.json`，并且任务只修改 `.kw/project-capabilities.json`、`.kw/project-skills.json`、`.kw/policies/**` 或 `.kw/project-agent-permissions.json`，切换到 `kw-project-capability`。

## Triage

1. 读取请求的 package root，并查找 `capability-package.json`。
2. 如果 manifest 在 KW workspace root，将其视为 legacy/scattered layout：保持兼容，但新的 package source 应迁移到 `capability-packages/<package-id>/`。
3. 如果 package source 已位于 `capability-packages/<package-id>/`，package-only 文件留在该目录，并用 v2 `recipe` mappings 投影 canonical repo facts。
4. 如果 canonical `knowledge/**`、`specs/**` 或 `examples/**` 应继续保留在 repo root，通过 `recipe.source_roots` 和 `recipe.mappings` 投影；不要复制到 package root 下。

## Authoring Root

新的 publishable packages 使用：

```text
capability-packages/<package-id>/
  capability-package.json
  capability/profile.json
  skills/project-skills.json
  policies/**
  validators/**
  evals/**
```

Root-level `capability-package.json`、`capability/` 和 `skills/` 只作为 compatibility input 保留。不要创建 source `payload/**`；`kw control capability pack` 负责 generated payload staging。

## Commands

- Validate: `kw control capability validate --path capability-packages/<package-id>`
- Pack dry-run: `kw control capability pack --path capability-packages/<package-id> --dry-run`
- Pack staging: `kw control capability pack --path capability-packages/<package-id> --output-dir <dir>`
- Publish dry-run: `kw control capability publish --path capability-packages/<package-id> --dry-run --registry-url <registry>`
- Install check: `kw control capability install --package-tar <staging-dir> --package-id <package-id> --version <version> --overwrite`

Consumer scripts 可以包一层这些命令来固定 registry、output directory 或 dogfood 参数，但不得重新实现 payload selection、checksums、publish 或 install verification。

## Verification

完成 package change 前，记录 explicit evidence：file selection、redaction、publishability、i18n impact、`validate`、pack dry-run、temporary consumer install、lock contents、generated project skill output、policy/validator entrypoints 和 change validation。
