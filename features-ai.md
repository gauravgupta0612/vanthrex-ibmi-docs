---
layout: default
title: "AI assistant"
nav_order: 12
parent: "Features"
---

# AI assistant (`@vanthrex`)
{: .no_toc }

An IBM i expert in the VS Code chat: explain, document, review and modernize RPG, write Db2 for i SQL against your real tables, and fix compile errors. New in 0.6.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## What it is

Type **@vanthrex** in the VS Code chat and ask in plain language, or start with a command:

| Command | What it does |
|---|---|
| `/explain` | Explains the selected code or the open source: purpose, inputs and outputs, files and programs used, main flow |
| `/document` | Adds a program header and a comment above each procedure, without changing the logic |
| `/review` | A prioritised list of bugs, error-handling gaps, performance and security issues, with fixes |
| `/modernize` | Rewrites fixed-format or old-style code as modern `**FREE` RPG with the same behaviour |
| `/test` | Generates RPGUnit tests for a procedure, with the command to build them |
| `/fix` | Explains each compile error of the open source and gives the corrected code |
| `/sql` | Writes a Db2 for i statement from a description, using your **real** tables and columns |
| `/object LIB/NAME *TYPE` | Explains an object: what it is, who uses it, what it touches |

Examples:

- `@vanthrex /sql customers in Paris with more than 5 open orders, newest first`
- `@vanthrex why is my job ORDBATCH waiting?`
- `@vanthrex /object APPLIB/ORDENTRY *PGM`
- Select a subroutine → right-click → **Vanthrex AI → Explain**

## Why it helps

- **It knows your system.** The assistant sees the connected system's name, IBM i release and library list.
- **It looks things up instead of guessing.** It can describe objects (attributes, source, table columns and indexes, bound modules), read source members, search objects, check the system status (CPU, disk, jobs in MSGW, QSYSOPR messages) and run read-only queries.
- **It works where you work.** Right-click in a source, the 💡 on a compile error, or right-click an object in the Libraries view.

## How to use it

1. You need a chat model in VS Code — for example **GitHub Copilot Chat** (any model you select in the chat works).
2. Connect to an IBM i in Vanthrex (the assistant also answers general questions without a connection, but can't look anything up).
3. Open the chat and type **@vanthrex**, or use:
   - right-click in an RPG, CL, DDS, COBOL or SQL source → **Vanthrex AI** → *Explain*, *Document*, *Review*, *Modernize*, *Unit tests*, *Fix compile errors*, *Write SQL*;
   - the 💡 on an IBM i compile error → **Ask AI to explain and fix this compile error**;
   - right-click an object → **AI: Explain This Object**;
   - the quick menu (**Ctrl+Alt+I**) → *Ask the IBM i AI assistant*.
4. SQL answers have buttons to **open the statement in a SQL scratchpad** and to **Explain its performance**.

## Safety

- The assistant **only reads**. A query must be a single `SELECT`, `WITH` or `VALUES` statement; statements that change data and functions with side effects (for example `QCMDEXC`, `IFS_WRITE`, `GENERATE_SPREADSHEET`) are refused.
- Vanthrex **asks before each query** and before reading an IFS file (turn query confirmations off with `vanthrex.ai.confirmQueries` if you prefer).
- When the assistant suggests a change (an UPDATE, a new program), it writes it for you to review — it never runs it.
- **Your code goes to the language model you selected** in VS Code chat, under that provider's terms. Turn the assistant off with `vanthrex.ai.enabled`, or stop it from looking things up with `vanthrex.ai.useTools`.

## Copilot agent mode

The assistant's tools are also available to GitHub Copilot in agent mode and can be referenced in any prompt:

| Tool | Reference | What it does |
|---|---|---|
| IBM i: Run read-only SQL | `#ibmiQuery` | Runs one read-only query and returns up to 200 rows |
| IBM i: Read source member | `#ibmiSource` | Reads `LIB/FILE(MEMBER)` or an IFS stream file |
| IBM i: Describe object | `#ibmiObject` | Attributes, source, columns, indexes and modules of an object |
| IBM i: Search objects | `#ibmiSearch` | Finds objects by name or text in the library list |
| IBM i: System status | `#ibmiStatus` | CPU, disk, jobs waiting for a reply, latest QSYSOPR messages |

## Settings

| Setting | Default | Purpose |
|---|---|---|
| `vanthrex.ai.enabled` | `true` | Turn the assistant and the AI commands on or off |
| `vanthrex.ai.useTools` | `true` | Let the assistant look things up on the connected IBM i |
| `vanthrex.ai.allowQueries` | `true` | Let the assistant run read-only queries |
| `vanthrex.ai.confirmQueries` | `true` | Ask before each query |
| `vanthrex.ai.maxSourceChars` | `60000` | Largest amount of source sent in one request |
