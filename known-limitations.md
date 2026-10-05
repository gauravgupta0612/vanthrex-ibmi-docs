---
layout: default
title: Known limitations
nav_order: 10
---

# Known limitations (0.6)

- **Several systems** can be connected, but the views show one (the active) system at a time.
- **Where used** builds its cross-reference with DSPPGMREF in QTEMP, so it needs a Mapepire SQL engine (not db2util). Scanning large libraries takes a while.
- **Source dates and conflict checks** need a Mapepire SQL engine. With db2util, members are copied as plain text and dates are reset on save.
- **Long lines:** lines longer than the source file's record length can't be saved; the save stops and the previous version is kept.
- **Table data editor** writes each change straight away (no commitment control). Rows are identified by relative record number, so don't reorganize a file while editing it.
- **Rename** only works inside one source and refuses length changes in fixed-format sources, because they would shift columns.
- **Fixed → free converter** converts H, F, D, P and C specs; I and O specs and primary/table files are left with a `// TODO`.
- **Generate SQL (DDL)** needs a Mapepire SQL engine.
- **Extract to procedure** works on whole lines of free-form calculations and creates a procedure without parameters.
- **Library compare** decides "different" from line counts, change dates, sizes and source timestamps; it does not read object contents.
- **Debugger** needs the IBM i Debug Service and IBM's IBM i Debug extension, and debugs programs in a batch job (no service entry points or 5250 screens yet) — see [Debugging](debugging.md).
- **AI assistant** needs a chat model in VS Code (for example GitHub Copilot Chat). The code you ask about is sent to that model. Its read-only check blocks known side effects, but user-defined SQL functions can do anything — that is why Vanthrex asks before every query.
- **Call graph** and **SQL Explain** need a Mapepire SQL engine. The call graph can't see dynamic calls (program names in variables).
- **Git sync** compares member change times and text; it does not track renamed or deleted members (deleted members are reported and kept in the repository).
- **Interactive (5250) commands** such as `WRKACTJOB` can't run from the CL runner; use their `OUTPUT(*PRINT)` form or the IBM i Services SQL snippets (type `ibmi-` in a `.sql` file).

Have an idea or hit a limit that blocks you? [Open an issue](https://github.com/gauravgupta0612/silverlake-ibmi/issues/new/choose).
