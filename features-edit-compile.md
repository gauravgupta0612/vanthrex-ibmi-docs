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

**What it is:** Converts fixed-format RPG IV into free format:

| Fixed | Free |
|---|---|
| H-spec | `ctl-opt …;` |
| F-spec | `dcl-f name [device] [keyed] [usage(…)] keywords;` — program-described files get `disk(len)` and `keyed(*char:len)` |
| D-spec S / C | `dcl-s` / `dcl-c` with the free-form type (`char`, `varchar`, `packed`, `zoned`, `int`, `date(*ISO)`, `pointer`, `ind`…) |
| D-spec DS | `dcl-ds … end-ds;` — subfields with `pos(n)`, `OVERLAY` on the DS → `pos`, externally described DS, LIKEDS without END-DS |
| D-spec PR / PI | `dcl-pr … end-pr;` / `dcl-pi … end-pi;` with parameters (`dcl-parm` when a name is also an op code) |
| P-spec | `dcl-proc name [export]; … end-proc;` |
| C-spec | free-form calculations with indentation, indicator handling and `%FOUND` / `%EOF` checks |

Long names (`...`), continued keywords and literals are joined, compiler directives stay where they are, compile-time data (`**CTDATA`) is left untouched, and long statements are wrapped at column 80.

**How:** Select the lines → right-click → **Convert Fixed Format to Free (H, F, D, P and C Specs)**, or run it with nothing selected to convert the whole source. Anything it can't convert safely is marked `// TODO` (I and O specs, primary/table files). To restructure the code as well, ask **@vanthrex /modernize** — see [AI assistant](features-ai.md).

## Local history and compare

**What it is:** A local copy of every member and IFS file you open or save.

**How:** Right-click inside a member and pick one of:

- **Show Local History:** choose a version → **Compare** or **Restore**.
- **Compare with Copy on IBM i:** see your unsaved changes, or someone else's changes on the server.
- **Compare with Another Member:** for example DEV against PROD (`PRODLIB/QRPGLESRC(ORDENTRY)`).

In the tree, right-click a member → **Select for Compare**, then right-click another → **Compare with Selected**.
