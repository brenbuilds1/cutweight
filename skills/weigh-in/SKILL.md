---
name: weigh-in
description: >
  Weigh an agent setup and print a fight-card receipt. Use when asked to weigh
  in, weigh my agent, check my agent's weight or token overhead, or compare
  before and after a cut. Measures the always-on context bill (installed
  skills, memory files, MCP tool schemas), assigns a weight class, prints a
  shareable card, and shows the delta against the last weigh-in. Read-only
  except for its own append-only log.
---

# Weigh-In

The scale for your agent. skill-diet finds what to cut; weigh-in tells you
what you weigh, before the cut and after it. Step on the scale first, cut,
step on it again.

## Method

1. Measure the always-on bill exactly as skill-diet does: installed skills
   (frontmatter name plus description each), memory files loaded at session
   start (CLAUDE.md, AGENTS.md, local variants, imports), MCP tool schemas
   (eager-loaded only; a server you cannot enumerate is unknown, never zero).
2. Rough tokens for English markdown: characters / 3 on Claude models with
   the Opus 4.7 tokenizer (Opus 4.7+, Sonnet 5, Fable 5), characters / 3.5
   to 4 on older Claude and GPT-style tokenizers. Label estimates.
3. Read the last card from `.cutweight/weigh-ins.md` if it exists. Compute
   the delta.
4. Print the card. Append it to the log. Never edit old cards.

## Weight Classes

Cutweight's own scale, by always-on tokens per message:

| class | always-on |
|---|---|
| flyweight | under 1,000 |
| lightweight | under 3,000 |
| middleweight | under 8,000 |
| heavyweight | under 20,000 |
| superheavyweight | 20,000 and up |

## The Card

```text
cutweight weigh-in: 2026-07-10
always-on: 7,412 tokens on every message
  skills: 3,509 (27 installed)
  memory files: 3,903
  mcp schemas: ~0 (deferred loading)
class: middleweight
last weigh-in: 9,180 (-19%, was heavyweight)
next cut: the 25-skill plugin billing 2,462 for 4 skills used
```

Keep the card under 12 lines. It is made to be posted.

## Hard Rules

- The log is append-only. A rewritten history is not a weigh-in.
- Measured or labeled-estimate numbers only.
- The card always names the single next cut, or says "at weight" if lean.
- Never name an agent-maintained memory file (auto-memory index, session
  memory) as the next cut. Bill it on the card, flag it to its owner. Its
  lines are the agent's retrieval keys; hand-trimming them breaks recall.
- A card meant for posting shows counts and categories, never private tool,
  server, or plugin names. Generalize anything internal before it leaves
  the machine.
- Keep `.cutweight/` out of version control; the log stays on the machine.
- Weigh-in changes nothing but its own log. The human does the cutting.
