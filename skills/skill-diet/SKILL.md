---
name: skill-diet
description: >
  Audit the always-on context cost of an agent setup: installed skills, memory
  files (CLAUDE.md, AGENTS.md), and MCP tool schemas. Use when asked to audit,
  trim, shrink, or cut skills or context, when an agent picks the wrong skill
  or feels dumber after the setup grew, when MCP servers eat the context
  window, or when the token bill grows without more work getting done.
  Produces a keep/trim/cut table with measured numbers. Does not delete
  anything.
allowed-tools: Read Grep Glob
---

# Skill Diet

Skill descriptions, memory files, MCP tool schemas: your agent reads all of
it on every message before any work happens. Caching makes that cheap in
dollars. It still fills the context window, and full windows measurably
degrade output. This skill reads the whole bill.

## When To Use

After installing a skill pack or connecting an MCP server. When the agent
picks the wrong skill. When the bill grows without more work done.

## Method

Rough tokens for English markdown: characters / 3 on Claude models carrying
the Opus 4.7 tokenizer (Opus 4.7+, Sonnet 5, Fable 5), characters / 3.5 to 4
on older Claude (Sonnet 4.6, Haiku 4.5) and on GPT-style tokenizers. The
newer Claude tokenizer counts roughly 30% higher, varying by content, so
never reuse counts across models. When exact matters, Anthropic's
count-tokens endpoint is free and per-model; for GPT, tiktoken runs locally.
Label every number measured or estimated.

1. Skills. Find every installed skill: `~/.claude/skills`, `.claude/skills`,
   `~/.codex/skills`, `.agents/skills`, plugin directories. Record two
   numbers each: always-on (frontmatter name plus description, injected into
   every request) and on-trigger (body plus every file it tells the agent to
   read).
2. Memory files. Find everything loaded at session start: CLAUDE.md and
   AGENTS.md at user level, project level, subdirectories, local variants,
   plus files they import. All always-on. Measure each. Leave style linting
   to linters; the job here is the bill. Files a human wrote (CLAUDE.md,
   AGENTS.md) are fair to trim. Files an agent maintains for itself
   (auto-memory indexes, session memories) get billed, NEVER hand-trimmed:
   their lines are retrieval keys, and cutting them breaks the agent's
   recall in ways that surface weeks later. If one must shrink, the owning
   agent compacts it in-context.
3. MCP tool schemas. Usually the biggest line item: each connected server
   injects its tool catalog into every request, commonly 500-1,400 tokens
   per tool. List servers from `.mcp.json` and client settings, count each
   server's tools, estimate schema cost. If the client defers tool loading
   (tool search, lazy loading), bill only what loads eagerly and say so. A
   server you cannot enumerate is unknown, never zero.
4. Overlap and dead weight (skills). Name pairs claiming the same trigger
   phrases. If session history exists, list skills that never fired;
   otherwise ask the user and mark the rest unknown, not unused.
5. Read the fattest items. Rules earn their tokens. Backstory does not.

## Output Shape

```markdown
| item | kind | always-on | on-trigger | notes | verdict |
|---|---|---|---|---|---|
| github (94 tools) | mcp | 17,600 | - | eager-loaded | trim: disable unused toolsets |
| CLAUDE.md (project) | memory | 3,900 | - | half is lint rules | trim: linters enforce those |
| seo-writer | skill | 71 | 18,400 | never fired | cut: dead |
| commit-helper | skill | 62 | 1,410 | overlaps git-flow | keep |
```

Close with three totals: always-on today, always-on after the cuts, what that
saves on every single call.

## Trim Moves

- Disable MCP servers you rarely use; reconnect when needed. Disable per
  project where the client allows: a server idle in this repo may be
  load-bearing in another. Prefer clients that defer tool loading.
- Cut memory-file rules a linter or formatter already enforces.
- Move backstory and examples out of skill bodies and human-authored memory
  files into reference files fetched on demand.
- Merge colliding skills, or sharpen both descriptions until triggers stop
  overlapping.
- Delete the duplicate when something is installed at user and project
  level. Cut your user-level copy first: the project copy may be the team's,
  and cutting it from a shared repo cuts it for everyone.

## Hard Rules

- Never delete or edit anything. Output the list, the human cuts.
- Measured numbers only; estimates get labeled. No benchmark folklore.
- No fire history available means unknown, not unused.
- Every verdict says why: overlap, dead, fat body, duplicate, eager schemas.
