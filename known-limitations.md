---
layout: default
title: Known limitations
nav_order: 9
---

# Known limitations (0.3)

- **One active connection at a time.**
- **Where used** builds its cross-reference with DSPPGMREF in QTEMP, so it needs a Mapepire SQL engine (not db2util). Scanning large libraries takes a while.
- **Source dates and conflict checks** need a Mapepire SQL engine. With db2util, members are copied as plain text and dates are reset on save.
- **Long lines:** lines longer than the source file's record length can't be saved; the save stops and the previous version is kept.
- **Table data editor** writes each change straight away (no commitment control). Rows are identified by relative record number, so don't reorganize a file while editing it.
- **Rename** only works inside one source and refuses length changes in fixed-format sources, because they would shift columns.
- **Fixed → free converter** handles C-specs only (H/F/D specs are left as they are). Anything it can't convert safely is marked `// TODO`.
- **Interactive (5250) commands** such as `WRKACTJOB` can't run from the CL runner; use their `OUTPUT(*PRINT)` form or the IBM i Services SQL snippets (type `ibmi-` in a `.sql` file).

Have an idea or hit a limit that blocks you? [Open an issue](https://github.com/gauravgupta0612/silverlake-ibmi/issues/new/choose).
