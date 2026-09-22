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

cutweight is one dial and three tools. Weigh in first. Cut. Weigh in
again. Post your card.

## The Dial

### cutweight

`/cutweight light | full | ultra | off`. One setting for the two things
billed on every message: the words in the reply and the thinking behind
it. Answers like a cornerman between rounds, keeps commands, code, file paths,
and error strings exact, caps thinking on light tasks only after verifying
quality held, and checks the live round before calling a fact that may
have changed.

Path: [`skills/cutweight/SKILL.md`](./skills/cutweight/SKILL.md)

## The Tools

### cutweight-weigh

The scale. Measures your always-on bill (skills, memory files, MCP
schemas), assigns your weight class from flyweight to superheavyweight,
prints a shareable fight card, and tracks the delta against your last
weigh-in in an append-only log.

Path: [`skills/cutweight-weigh/SKILL.md`](./skills/cutweight-weigh/SKILL.md)

### cutweight-diet

Reads the whole bill: what every installed skill, memory file, and MCP
server costs always-on and on-trigger, which skills fight over the same
triggers, which never run. Hands you a keep/trim/cut table. Deletes
nothing.

Path: [`skills/cutweight-diet/SKILL.md`](./skills/cutweight-diet/SKILL.md)

### cutweight-cut

Cuts the session before the context wins. One task per session, /clear
between tasks, /compact only to continue the same one, a five-line handoff
note before every reset, and the tells that say the context is now working
against you.

Path: [`skills/cutweight-cut/SKILL.md`](./skills/cutweight-cut/SKILL.md)

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
cp -R skills/cutweight ~/.claude/skills/
```

## Renamed in 2.0

Every command now carries the brand, so the family reads as one thing in
hosts without namespaces: `skill-diet` is `cutweight-diet`, `weigh-in` is
`cutweight-weigh`, `session-cut` is `cutweight-cut`, and `word-diet` plus
`think-light` merged into the `cutweight` dial. Old folder names no longer
update; reinstall to get the new ones.

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
  cutweight/
    SKILL.md
  cutweight-cut/
    SKILL.md
  cutweight-diet/
    SKILL.md
  cutweight-weigh/
    SKILL.md
```

Flat by design.

cutweight's own weight: the four skill descriptions add roughly 320
always-on tokens to your setup. A diet that hides its own calories is not
a diet.
