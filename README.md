# ViBo skills

Six SKILL.md definitions for AI agents, from the ViBo modular agent network:
memory, web compression, thread memory, archive, privacy proxy and live handoff.

Each file is a self-contained skill definition — when to use it, what it takes,
what it returns, and the rules the agent must follow. They follow the open
SKILL.md format and work with any agent that reads it.

## Skills

| Skill | What it does |
|---|---|
| [`memory`](skills/memory/SKILL.md) | facts survive between sessions; public, private and secret tiers |
| [`web-compression`](skills/web-compression/SKILL.md) | a page is reduced to the part that answers the question |
| [`thread-memory`](skills/thread-memory/SKILL.md) | long conversation stays on disk, the model reads a summary |
| [`archive`](skills/archive/SKILL.md) | documents packed into one searchable file |
| [`privacy-proxy`](skills/privacy-proxy/SKILL.md) | secrets masked before a prompt reaches a provider |
| [`handoff`](skills/handoff/SKILL.md) | a snapshot that lets work resume after a restart |

## About the implementations

These are the public skill definitions. The runtime package — storage engine,
licence activation, proxy and CLI — is distributed separately under a commercial
licence at https://wwwvibo.com. Nothing here requires it: the definitions are
readable on their own, and a free, dependency-free implementation of the memory
discipline is published as
[Agent Memory Protocol](https://github.com/vnbochkarev-netizen/vibo-memory-protocol).

## Design notes

The tiering rule is the important part: a secret is never a stored value, only the
name of an environment variable. Everything else follows from keeping the model
context small — recall returns few rows, pages are compressed before they enter,
threads are summarised rather than resent.

## Layout

```
skills/
  memory/SKILL.md
  web-compression/SKILL.md
  thread-memory/SKILL.md
  archive/SKILL.md
  privacy-proxy/SKILL.md
  handoff/SKILL.md
```

## Licence

The skill definitions in this repository are published under CC BY 4.0 — use them,
adapt them, keep the attribution. The ViBo runtime is commercial and licensed
separately.
