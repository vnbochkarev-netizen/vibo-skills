---
name: vibo-handoff
description: "Save a snapshot of the running task and resume it after a restart, a crash or a new session. Use when work must survive the end of a conversation."
---

# Live handoff

One snapshot, overwritten every time: what the task is, what is done, what comes next,
what is waiting on a decision. After a restart the agent asks whether to continue and
picks up from the same point.

## When to use

- before the session ends, a restart or a context reset;
- when work is paused waiting for the user;
- when a second agent takes over.

## Commands

```bash
vibo save-state "migrate demo to v9.23" --done "db dump" --next "smoke test" --waiting "owner approval"
vibo resume
vibo resume --json
```

## Rules for the agent

1. Ask before restoring a snapshot into a new context: it reintroduces earlier content.
2. Never put a secret in the snapshot — only the placeholder or the variable name.
3. Keep one snapshot; overwrite it rather than growing a log.
4. Update it at every stop, not on request.

## Why it matters

An agent without a handoff asks "what were we doing?" on the first message of every
session. That question is a product failure, not a user problem.
