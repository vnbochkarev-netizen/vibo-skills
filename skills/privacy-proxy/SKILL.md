---
name: vibo-privacy-proxy
description: "Mask API keys, passwords and tokens before a prompt reaches any LLM, using an OpenAI-compatible local proxy. Use when the user works with secrets around a model provider."
---

# Privacy layer

An OpenAI-compatible proxy that sits between the agent and the provider. Registered
secrets are encrypted at rest, replaced with a placeholder in the outgoing prompt, and
counted in the response audit.

## When to use

- the agent handles credentials alongside prompts;
- the user works under a data-handling policy;
- a leaked key in a log would be a real incident.

## How it works

1. Register a secret once: `POST /secrets {name, value}` — stored as ciphertext.
2. Point the agent's base URL at the proxy: `http://localhost:8017/v1` (self-hosted).
3. The proxy replaces known secrets with a placeholder, plus a pattern fallback
   (`sk-…`, `ghp_…`, `password=…`).
4. Every response reports how many secrets were blocked and how many tokens were
   never sent.

## Rules for the agent

1. Default to self-hosted. The hosted mode sends prompts through a third party —
   an explicit opt-in, never a default.
2. Never make the proxy the only route to a model: if it stops, the agent must fall
   back to the direct provider.
3. Report the audit line after a proxied call.
4. Protect the management endpoint with an admin token.

## Honest limit

Only registered secrets and known key patterns are masked. The rest of the prompt is
forwarded as-is, because the model has to read it to answer.
