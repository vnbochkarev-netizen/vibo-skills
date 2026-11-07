---
name: vibo-thread-memory
description: "Keep a long conversation whole on disk while the model reads a summary, and restore details on demand. Use when a thread grows past roughly fifty messages."
---

# Thread memory

Long threads are expensive to resend and easy to lose. The full history stays in a
local file; the model gets a compressed context; any detail is one query away.

## When to use

- a conversation passes ~50 messages or a large share of the context window;
- the user asks what was agreed days ago;
- the agent is about to start a fresh session and needs to carry the thread over.

## Commands

```bash
vibo dialog add "client asked about pricing, we agreed $9 one-time" --role assistant --topic pricing
vibo dialog compress
vibo dialog context
vibo dialog ask "what did we agree about pricing?"
```

## Rules for the agent

1. Compress before the context is full, not after.
2. Keep the full file; never delete history to save space.
3. When the user asks for a detail, query the file instead of guessing.
4. Tell the user the reduction in one line.

## Measured

Reference thread: 72% fewer tokens on the conversation, full history retained.
