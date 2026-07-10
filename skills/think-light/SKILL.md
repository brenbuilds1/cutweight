---
name: think-light
description: >
  Cut reasoning-token weight. Use when thinking or reasoning tokens dominate
  the bill, when asked to cap a thinking budget, lower effort, or stop simple
  tasks from burning extended thinking. Light tasks get light thinking:
  matches thinking budget to task weight, then verifies accuracy held before
  keeping any cap. Never caps blind.
---

# Think Light

Reasoning tokens bill like output tokens, and models usually lock their
answer early in the chain; the tail is often narration you pay for. Light
tasks get light thinking. Save the heavy reasoning for the problems that
are actually heavy.

## Method

1. Sort your recurring tasks into two piles:
   - light: lookups, renames, formatting, single-file edits, commit messages,
     questions with one right answer. Extended thinking rarely changes these.
   - heavy: multi-file refactors, architecture calls, debugging across
     boundaries, anything where the first idea is usually wrong. Thinking
     earns its tokens here.
2. Cap the light pile. Use your agent's thinking controls: effort levels,
   a thinking-budget setting, or per-request flags. Cut the budget hard for
   light tasks; leave heavy tasks alone at first. Prefer per-session or
   per-request controls: a cap written into settings outlives the task, and
   a cap in project settings caps your teammates too. Never ship a cap in
   shared config.
3. Verify before keeping. Rerun two or three recent real tasks from the
   capped pile and compare results against what you got uncapped. Same
   quality: keep the cap. Worse: raise it back and say so.
4. Log what you capped and the before/after spend in the weigh-in log, so
   the saving is a receipt, not a feeling.

## Hard Rules

- Never keep a cap you did not verify on real tasks.
- Caps are per task type. A global cap is a blind cap.
- If quality dropped, the cap loses. Raise it back without ceremony.
- Record the cap and the saving. Unmeasured savings do not exist.
