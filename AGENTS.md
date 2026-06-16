# AGENTS.md — orientation for AI coding agents

This repository is **not an application** — it is a portable **Agent Skill** that teaches an AI
agent to operate [renef](https://renef.io) (a dynamic-instrumentation engine for Android ARM64:
hook native/Java functions, scan/patch memory, trace syscalls, bypass SSL pinning / root detection
via Lua 5.4 scripts).

## What to read

The skill itself is the source of truth:

- **`skills/renef/SKILL.md`** — operator's manual: syntax contract, self-lint, task → playbook.
- **`skills/renef/references/`** — load on demand:
  - `lua-api.md` — full Lua API (Module, Memory, hook, Jni, Java, Thread, File, Syscall, OS, KCov)
  - `cli.md` — CLI commands, flags, connect modes, build/deploy
  - `from-other-tools.md` — translate Frida JS and GameGuardian (`gg.*`) / game-hacking Lua → renef
  - `recipes.md` — copy-paste scripts (SSL/root bypass, tracing, memory cheats, CTF)
  - `gotchas.md` — pitfalls, doc/runtime discrepancies, troubleshooting

If a user asks you to write or fix a renef script, **read `skills/renef/SKILL.md` first**, then pull
the relevant reference file. The format is progressive-disclosure by design — do not load all
references at once.

## Format

`SKILL.md` uses the standard **Agent Skills** format (YAML frontmatter with `name` + `description`).
This is consumed natively by Claude Code and OpenCode, and the content is plain Markdown reusable by
any agent. See `README.md` → **Install** for per-agent setup.

## Installing this skill for the user

When a user wants the renef capability available in their own projects, copy the skill directory
into a location their agent scans (one copy can serve multiple agents):

```bash
# Works for BOTH Claude Code and OpenCode (both read .claude/skills):
mkdir -p ~/.claude/skills && cp -r skills/renef ~/.claude/skills/renef   # global
# or, per-project:
mkdir -p .claude/skills && cp -r skills/renef .claude/skills/renef
```

This repo ships **documentation/instructions only** — no renef binaries. renef itself
(server/agent) is installed separately on the Android device; see `skills/renef/references/cli.md`.
