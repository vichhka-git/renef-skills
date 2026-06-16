# renef-skills

A [Claude Code](https://claude.com/claude-code) **plugin** that makes AI agents **operate
[renef.io](https://renef.io) correctly** — the dynamic-instrumentation engine for **Android
ARM64**: hook native & Java functions, scan/read/write/patch process memory, trace syscalls, and
bypass SSL pinning / root detection through **Lua 5.4** scripts (memfd injection, no ptrace).

This is an operator's manual, not a tutorial. An agent that can already write Frida hooks,
GameGuardian (`gg.*`) cheats, or game-hacking Lua has the *concepts* — it just lacks renef's exact
**syntax and workflow**, and without it emits Frida JavaScript, dotted Java class names, absolute
hook addresses, `retval.replace()`, or `gg.*` calls, none of which work in renef. The skill gives
the agent a precise **syntax contract**, a **self-lint** to run over its own scripts, a **task →
playbook** map, translation tables from other tools, and copy-paste recipes.

## What's inside

```
renef-skills/
├── .claude-plugin/
│   └── plugin.json                # plugin manifest
├── CONTRIBUTING.md                # how to contribute VERIFIED findings (no confidential target data)
└── skills/
    └── renef/
        ├── SKILL.md                # operator framing: roles, syntax contract, self-lint, task playbook
        ├── probe.lua               # RUN FIRST — ground-truths the API/behavior of your renef build
        └── references/
            ├── methodology.md      # the investigation loop: solve a NEW bypass yourself
            ├── debugging.md        # renef hides errors — recover them; failure-symptom table; hot-hook race; RASP
            ├── lua-api.md          # full Lua API: Module/Memory/hook/Jni/Java/Thread/File/Syscall/OS/KCov
            ├── cli.md              # commands, flags, connection modes, build/deploy, companion tools
            ├── from-other-tools.md # translate Frida JS + GameGuardian (gg.*) / game-hacking Lua → renef
            ├── recipes.md          # worked examples: SSL/root bypass, WebView, tracing, memory, CTF…
            └── gotchas.md          # pitfalls, doc/runtime discrepancies, troubleshooting
```

The skill uses **progressive disclosure**: `SKILL.md` stays compact (the model loads it when a task
involves renef), and the larger reference files are pulled in only when needed.

## Install

This is a standard **Agent Skill** (`SKILL.md` with `name` + `description` frontmatter). It is
loaded **on demand** — the agent sees the skill's description and pulls in the full content only
when a task involves renef.

> **One copy, two agents.** Both **Claude Code** and **OpenCode** read the `.claude/skills/`
> directories. Installing into `~/.claude/skills/renef/` (global) or `.claude/skills/renef/`
> (per-project) makes the skill work in **both** with no conversion.

### Claude Code & OpenCode (recommended)

```bash
# Global — available in all your projects, for both Claude Code and OpenCode:
mkdir -p ~/.claude/skills && cp -r skills/renef ~/.claude/skills/renef

# Or per-project:
mkdir -p .claude/skills && cp -r skills/renef .claude/skills/renef
```

Then just describe a renef task — the skill activates automatically (in OpenCode it's exposed via
the native `skill` tool).

**OpenCode-native locations** also work if you prefer them: `.opencode/skills/renef/SKILL.md`
(project) or `~/.config/opencode/skills/renef/SKILL.md` (global). OpenCode additionally scans
`.agents/skills/` and `~/.agents/skills/`.

### Claude Code as a plugin
Add this repo as a plugin source (or to a marketplace you control) and enable the `renef` plugin —
the bundled skill registers automatically. (`.claude-plugin/plugin.json` is the manifest.)

### Other agents (Cursor, Aider, Cline, Codex, …)
Skill auto-discovery isn't universal yet. Two portable options:

1. **Point the agent at this repo** — `AGENTS.md` (read by many agents, incl. OpenCode/Cursor/Zed)
   orients it to the project and tells it to read `skills/renef/SKILL.md`.
2. **Reference the markdown directly** in the agent's rules/instructions (e.g. a Cursor
   `.cursor/rules/*.mdc` that includes `skills/renef/SKILL.md`). The content is plain Markdown.

## Usage

Just describe the task — the skill triggers on renef-related work:

- "Write a renef script to bypass SSL pinning in com.example.app"
- "Port this Frida script to renef"
- "Hook the native `verify` function in libapp.so and log its args"
- "Use renef-strace to watch file access in this app"

## Scope & ethics

Renef targets **Android ARM64** and is for authorized security testing, app hardening review, CTFs,
and reverse-engineering of software you own or are permitted to analyze. Follow applicable law and
the target app's terms.

## Credits

- **renef** by [@ahmeth4n](https://github.com/Ahmeth4n/renef) — Apache-2.0. Docs: https://renef.io
- Community hooks: https://hook.renef.io · r2 plugin: https://github.com/ahmeth4n/r2renef ·
  auto-deploy module: https://github.com/vichhka-git/magisk-renef

This plugin is documentation/instructions only; it ships no renef binaries.
