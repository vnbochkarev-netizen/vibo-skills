---
name: vibo-web-compression
description: "Compress a web page to the part that answers the question before it enters the model context. Use when the agent would otherwise paste full articles into the prompt."
---

# Web compression

A fetched article is 5-15K tokens. Most of it does not answer the question. ViBo
keeps the relevant paragraphs and drops navigation, ads and duplicates.

## When to use

- the agent is about to read a page to answer one specific question;
- the same page is fetched more than once;
- the context window is filling with raw HTML.

## Commands

```bash
vibo web --compress https://example.com/article --query "pricing model"
```

## Rules for the agent

1. Compress before the page enters the prompt, never after.
2. Cache the summary by question; a repeat question costs nothing.
3. Never compress authenticated, internal or confidential pages without consent —
   the summary is written to a local cache.
4. Report what was saved, once, in one line.

## Measured

A 12,975-token article becomes 489 tokens (96.2% fewer) on the reference corpus.
Treat that as a measured example, not a promise for every page.
