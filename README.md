# .ai — Portable agent bootstrap kits

This folder installs the same governance layer — **skills + rules + memory + hooks + CI** — into any project, for any AI coding agent. One source of truth, one command, and a project goes from "an agent guesses at your standards" to "an agent has them in context, enforced at commit time."

The bootstrap is **conversational**: the agent detects your stack, asks about the project, audits every source file, then installs. You answer questions; it does the rest.

## What's in here

| Thing | What it is | Use when |
|---|---|---|
| [agent-kit/](agent-kit/) | Multi-agent kit — `AGENTS.md` + `.agents/`, `--target {agents,zcode,claude,all}`, memory cloned into the anchor file | **Default.** Any project, any agent (Claude Code included, via `--target all`) |
| [claude-kit/](claude-kit/) | The Claude-Code-only original — `CLAUDE.md` + `.claude/` | A Claude-only project, or maintaining an existing claude-kit install |
| [PROMPT_GENERATOR.md](PROMPT_GENERATOR.md) | Standalone prompt-structuring template | Turning messy intent into a structured codebase prompt |

---

## How to run it

### A. Recommended — conversational, phase-explicit

`cd` into the project you want to bootstrap, open your agent, and paste:

```
@/Users/mac/Projects/.ai/agent-kit/BOOTSTRAP.md

Bootstrap THIS project with the Agent Kit. Read BOOTSTRAP.md fully and follow every
phase exactly, in order, without skipping:
- Phase 0: confirm the working directory with me before any file operations.
- Phase 1: detect the stack(s) here — do not assume; if unsure, ask.
- Phase 2: ask me the context questions ONE AT A TIME.
- Phase 3: audit every source file line-by-line (background agents).
- Phases 4-6: install skills + rules + scripts + workflow, generate CLAUDE.md, set up
  memory, install the pre-commit hook, stage the CI workflow.
Apply the same depth and rigor the kit was built with. Do not commit anything. Do not
modify source code — only .claude/, CLAUDE.md, audits/, and the memory folder.
```

**Why this is the best way:** naming every phase is what keeps the agent honest. Terse invocations are where Phase 0 (directory confirmation), Phase 2 (one question at a time), and the line-by-line audit quietly get compressed into "install the files and declare victory."

Adjust the last line's write-scope list to your target: `.agents/` + `AGENTS.md` for `--target agents`, `.claude/` + `CLAUDE.md` for `--target claude`, both for `all`.

### B. Faster — script first, conversational finish

The mechanical half (detect stack, emit dirs, build rules, generate `AGENTS.md`, clone memory, install the plan-hook) runs instantly as a script:

```bash
bash /Users/mac/Projects/.ai/agent-kit/agent-init.sh . --target all
```

Then paste the block from **A** in your agent. It detects the mechanical install is already done and reduces Phase 4 to verification plus authoring `CLAUDE.md`, then continues with the context Q&A, audits, and memory.

### C. Minimal

```
@/Users/mac/Projects/.ai/agent-kit/BOOTSTRAP.md please bootstrap this project
```

Works, but this is exactly the invocation where phases get skipped. Prefer **A**.

### Claude-Code-only alternative

```
@/Users/mac/Projects/.ai/claude-kit/BOOTSTRAP.md please bootstrap this project
```

Uses [claude-init.sh](claude-kit/claude-init.sh) and writes `CLAUDE.md` + `.claude/` only. `agent-kit --target claude` produces the same shape and stays upgradeable to multi-agent later.

---

## Picking a `--target`

| Target | Writes | Read by |
|---|---|---|
| `agents` *(default)* | `AGENTS.md` + `.agents/{skills,scripts,rules.md}` | ZCode, Codex, Cursor, any `AGENTS.md` reader |
| `zcode` | above + `.zcode/{skills (symlinks),scripts,config.json}` | ZCode native |
| `claude` | `CLAUDE.md` + `.claude/{skills,scripts,rules.md}` | Claude Code |
| `all` | everything | all of the above |

`.agents/skills/` always holds the real files; `.zcode/skills/` symlinks into it, `.claude/skills/` are copies.

## What you get

- **7 skills** — `/x-implement`, `/x-check`, `/x-rules`, `/x-prompt`, `/x-check-file`, `/x-add-rule`, `/x-audit`
- **Rules** — universal baseline plus auto-detected stack modules (NestJS, Laravel, Django, FastAPI, Next.js, React, Vue, Nuxt, Flutter, React Native)
- **Anchor file** — `AGENTS.md` and/or `CLAUDE.md`, generated from your Phase 2 answers
- **Memory** — a per-project memory folder, **cloned verbatim into the anchor** so agents that don't auto-load memory still see it
- **Pre-commit hook** — pure bash, millisecond checks, blocks critical violations
- **CI** — `x-check.yml` staged into `.github/` alongside whatever's already there
- **Plan-mode hook** — per-target, plain text or JSON-wrapped
- **Audits** — `audits/<repo>/`, one line-by-line pass per detected repo

Full tables in [agent-kit/README.md](agent-kit/README.md) and [claude-kit/README.md](claude-kit/README.md).

## After bootstrap

```bash
bash /Users/mac/Projects/.ai/agent-kit/agent-sync.sh <project>   # propagate kit updates (keeps project-added rules)
bash <project>/.agents/scripts/install-hooks.sh all              # redeploy the pre-commit hook
bash <project>/.agents/scripts/install-workflows.sh all          # restage the CI workflow
bash <project>/.agents/scripts/clone-memory.sh <project>/AGENTS.md <memdir>   # refresh the memory clone
```

- **Add a rule** — edit `<project>/.agents/rules.md`, or use `/x-add-rule`. Project rules below the sentinel survive `agent-sync.sh`.
- **Add a skill** — drop `<name>/SKILL.md` into `<project>/.agents/skills/`.
- **Change the kit itself** — edit [agent-kit/rules/rules-baseline.md](agent-kit/rules/rules-baseline.md) or a stack module; future bootstraps pick it up, existing projects run `agent-sync.sh`.

## What it never does

Commit, push, modify your source code, run tests, install dependencies, configure linters, generate features, or replace existing CI. It stages; you commit.

---

**Updated:** 2026-08-16 · agent-kit v1.0 · claude-kit v1.1
