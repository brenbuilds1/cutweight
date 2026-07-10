# cutweight

Your agent is overweight.

Every message your agent processes carries skills that never fire, memory
files nobody trims, MCP schemas for tools you do not use, thinking tokens
that change nothing, and a transcript that gets heavier every round.
Caching makes most of that nearly free in dollars. Your agent still reads
all of it on every message, and measured quality drops as the window
fills: wrong tools get picked, instructions get forgotten, long sessions
degrade. Dead weight costs accuracy first, quota second, money a distant
third.

cutweight is five skills that cut it. Weigh in first. Cut. Weigh in again.
Post your card.

## The Skills

### Weigh-In

The scale. Measures your always-on bill (skills, memory files, MCP schemas),
assigns your weight class from flyweight to superheavyweight, prints a
shareable fight card, and tracks the delta against your last weigh-in in an
append-only log.

Path: [`skills/weigh-in/SKILL.md`](./skills/weigh-in/SKILL.md)

### Skill Diet

Reads the whole bill: what every installed skill, memory file, and MCP server
costs always-on and on-trigger, which skills fight over the same triggers,
which never run. Hands you a keep/trim/cut table. Deletes nothing.

Path: [`skills/skill-diet/SKILL.md`](./skills/skill-diet/SKILL.md)

### Word Diet

Puts the agent's replies on a diet. Answers like a cornerman between rounds:
zero filler, only what changes the next round, while the technical content
stays exact: commands, code, errors, citations. When facts are fresh or
likely to change, it checks the live round instead of calling it from old
tape.

Path: [`skills/word-diet/SKILL.md`](./skills/word-diet/SKILL.md)

### Think Light

Light tasks, light thinking. Sorts your tasks into light and heavy piles,
caps thinking budgets on the light pile, and only keeps a cap after
verifying on real tasks that quality held. Never caps blind.

Path: [`skills/think-light/SKILL.md`](./skills/think-light/SKILL.md)

### Session Cut

Cuts the session before the context wins. One task per session, /clear
between tasks, /compact only to continue the same one, a five-line handoff
note before every reset, and the tells that say the context is now working
against you.

Path: [`skills/session-cut/SKILL.md`](./skills/session-cut/SKILL.md)

## Install

Any agent (Claude Code, Codex, Cursor, Copilot, Gemini, Windsurf, more):

```sh
npx skills add brenbuilds1/cutweight
```

Claude Code, as a plugin:

```text
/plugin marketplace add brenbuilds1/cutweight
/plugin install cutweight@cutweight
```

Manual: copy folders under `skills/` into your agent's skills directory.
`.agents/skills/` is the most portable spot; Cursor and Codex also read
`~/.claude/skills/`.

```sh
cp -R skills/weigh-in ~/.claude/skills/
```

## Troubleshooting

- `npx: not recognized` or `command not found`: the skills CLI needs
  Node.js 18+. Install node, or skip npx entirely with the plugin or manual
  paths above.
- The plugin path runs inside Claude Code and needs no node on your PATH.
- The manual path needs nothing but a copy of this repo: every skill is one
  folder with one SKILL.md.

## Layout

```text
skills/
  session-cut/
    SKILL.md
  skill-diet/
    SKILL.md
  think-light/
    SKILL.md
  weigh-in/
    SKILL.md
  word-diet/
    SKILL.md
```

Flat by design.

cutweight's own weight: the five skill descriptions add roughly 700
always-on tokens to your setup. A diet that hides its own calories is not
a diet.
