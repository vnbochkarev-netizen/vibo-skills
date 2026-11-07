---
name: vibo-archive
description: "Pack documents into a single searchable archive, answer questions from it in milliseconds, and unpack it back to files. Use when an agent needs to work over a document set rather than a single file."
---

# Living archive

Documents are dead weight when they sit in folders. Pack them once into a `.vibo`
file: search by meaning, get the exact fragment, unpack when you need the originals.

## When to use

- the agent must answer from a set of contracts, specs, reports or presentations;
- a folder is too large to attach to the context;
- the same document set is queried repeatedly.

## Commands

```bash
vibo archive pack ./documents -o archive.vibo
vibo archive search archive.vibo "payment terms"
vibo archive list archive.vibo
vibo archive unpack archive.vibo -o restored
```

## Rules for the agent

1. Confirm before packing confidential or regulated documents — packing writes a
   second copy of the content into the archive file.
2. Return the fragment, not the whole document.
3. Keep the archive file where the user controls access to it.

## Formats

Markdown, text, DOCX, PDF (text layer), XLSX, PPTX and images with OCR. Configs and
binaries are filtered out.
