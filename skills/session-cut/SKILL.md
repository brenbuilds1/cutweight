---
name: session-cut
description: >
  Session-weight hygiene. Use when sessions run long, when an agent gets
  slower or starts forgetting mid-session, when deciding between /clear,
  /compact, or a fresh session, or when every message feels heavier than the
  work in it. Calls the moment a session has blown the weight limit: cut it
  right and start the next one light.
---

# Session Cut

Every message you send re-sends the conversation so far. The longer the
session, the heavier each message gets, and the older context starts working
against you. Knowing when to cut a session saves more tokens than any
single trim.

## The Calls

- One task, one session. Starting an unrelated task in an old session makes
  the new task carry the old one's weight.
- `/clear` between unrelated tasks. It is the cheapest reset there is.
- `/compact` only to continue the SAME task past context limits. Compaction
  is a summary; treat it as lossy, because it is.
- Fresh session with a handoff note beats a compacted haze. Before you
  clear, have the agent write five lines: what was done, what is next, which
  files matter. Paste that into the new session.

## The Tells

Cut the session when:

- The agent re-reads files it already read this session.
- It forgets or contradicts a decision made earlier in the session.
- Replies slow down or drift off the task you actually asked for.
- The work left is unrelated to the transcript behind it.

## Hard Rules

- Never /compact as a reflex. Ask first: is this the same task?
- The handoff note gets written before the clear, not remembered after.
- If the agent is fighting the context instead of the problem, cut the
  session. Reset.
