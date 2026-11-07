---
name: vibo-memory
description: "Persistent memory for an agent: facts survive between sessions, recall returns only the relevant rows, and a secret tier keeps credentials out of the model context. Use when the agent must remember users, projects, terms or decisions across sessions."
---

# Memory

Facts outlive the session. The agent keeps what the user told it, finds it by
meaning later, and sends the model a handful of relevant rows instead of a
transcript.

## When to use

- the user says something durable: a preference, a term, a decision, a client detail;
- the agent is about to ask a question it has already been answered;
- a fact needs correcting rather than duplicating.

## Three tiers

| Tier | What it holds | Rule |
|---|---|---|
| L1 public | names, cities, public project facts | safe to print |
| L2 private | notes, pricing, internal decisions | print only in the owner's private chat |
| L3 secret | keys, passwords, tokens | the value is never stored; only the environment variable name |

L3 is a pointer. `vibo add "API key" "env:MY_API_KEY" --level L3` records where the
secret lives, not the secret.

## Commands

```bash
vibo add "client anna" "pays on the 1st, PDF invoices"
vibo find "invoice terms anna"
vibo forget "client anna"
vibo stats
vibo usage
```

## Rules for the agent

1. Ask before storing anything; say where it goes and how to delete it.
2. Write the fact when it appears, not at the end of the session.
3. Search before asking the user again.
4. Never place a real secret in memory; store the variable name at L3.
5. Correct a fact by updating its label, never by adding a near-copy.

## Privacy

Memory is stored locally in the agent's working directory. No sync, no telemetry.
Forgetting one entry or deleting the store is the user's decision and takes one command.
