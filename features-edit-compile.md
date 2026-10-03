---
layout: default
title: "Edit & compile"
nav_order: 2
parent: "Features"
---

# Edit & compile
{: .no_toc }

Compile with one key, see errors on the right line, convert fixed format and never lose a version.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## One-key compile with inline errors

**What it is:** **Ctrl+Alt+C** compiles the open member or IFS file with the right command for its type (CRTBNDRPG, CRTSQLRPGI, CRTBNDCL, CRTPF, CRTDSPF…).

**Why it helps:** The compiler's errors land on the exact line and column, and in the Problems panel. You don't read a spool file.

**How:**

- **Ctrl+Alt+C** (or the 🚀 icon in the editor title).
- When several commands fit, choose once and it is remembered. **Compile With…** lets you choose again.
- Add your own commands in *Settings → Vanthrex: Compile Actions*, using variables such as `&LIB`, `&OBJLIB`, `&NAME` and `&SRCFILE`.

## Fixed → free format conversion

**What it is:** Converts fixed-format C-specs into free format, with indentation, indicator handling and `%FOUND` / `%EOF` checks.

**How:** Select the lines → right-click → **Convert Fixed-Format C-Specs to Free**. Anything it can't convert safely is marked `// TODO`.

## Local history and compare

**What it is:** A local copy of every member and IFS file you open or save.

**How:** Right-click inside a member and pick one of:

- **Show Local History:** choose a version → **Compare** or **Restore**.
- **Compare with Copy on IBM i:** see your unsaved changes, or someone else's changes on the server.
- **Compare with Another Member:** for example DEV against PROD (`PRODLIB/QRPGLESRC(ORDENTRY)`).

In the tree, right-click a member → **Select for Compare**, then right-click another → **Compare with Selected**.
