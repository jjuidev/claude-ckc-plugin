# claude-ckc-plugin

**Claude Kit Custom (`ckc`)** — companion plugin for [claudekit](https://github.com/anthropics/claude-code), bundling custom skills under the `/ckc:*` namespace.

Maintained by [jjuidev](https://github.com/jjuidev).

## Prerequisites

- [Claude Code](https://code.claude.com/docs) ≥ 2.x (Plugins GA)
- **claudekit** installed — `ckc` skills call shared skills (`docs-seeker`, `html-anything`, `ai-multimodal`) and the shared Python venv at `~/.claude/skills/.venv/bin/python3`.

## Install

### From GitHub (after publish)

```bash
# Inside Claude Code
/plugin marketplace add jjuidev/claude-ckc-plugin
/plugin install ckc
```

### Local development

```bash
claude --plugin-dir /Users/tandm/Documents/jjuidev/npm/ai-skills/claude-ckc-plugin
```

After editing any skill:

```
/reload-plugins
```

## Skills included

| Skill | Description |
|---|---|
| `/ckc:learn` | Learn a library/framework via structured research. Modes: `quick`, `full`, `detail`, `overview`, `cheatsheet`. Supports URL input and `--md`/`--html` output. |

## Usage examples

```text
/ckc:learn nextjs
/ckc:learn full tanstack-router
/ckc:learn cheatsheet zod
/ckc:learn https://orm.drizzle.team/docs/overview
```

## Add a new skill

1. Create `plugins/ckc/skills/<skill-name>/SKILL.md` with YAML frontmatter (`description:` required).
2. Drop assets into `plugins/ckc/skills/<skill-name>/references/`, `scripts/`, etc.
3. Reference assets with `${CLAUDE_PLUGIN_ROOT}/skills/<skill-name>/...`.
4. Bump `version` in `plugins/ckc/.claude-plugin/plugin.json`.
5. Commit & push — users get update via `/plugin update ckc`.

## Structure

```
.claude-plugin/
  marketplace.json          # marketplace catalog
plugins/
  ckc/
    .claude-plugin/
      plugin.json           # plugin manifest
    skills/
      learn/
        SKILL.md
        references/
        scripts/
```

This repo is a **marketplace containing one plugin** (`ckc`). To add more plugins later, drop them under `plugins/<name>/` and register them in `.claude-plugin/marketplace.json`.

## License

MIT © jjuidev
