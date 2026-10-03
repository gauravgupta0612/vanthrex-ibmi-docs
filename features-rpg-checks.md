---
layout: default
title: "RPG code checks"
nav_order: 7
parent: "Features"
---

# RPG code checks
{: .no_toc }

Warnings as you type, with quick fixes and per-rule switches.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## RPG code checks

**What it is:** Warnings as you type:

- unused variables
- GOTO
- a program with no `*INLR = *ON` or RETURN
- empty ON-ERROR blocks
- `SELECT *`
- numbered indicators
- overly long procedures
- fixed-format code mixed into free format

**Why it helps:** Mistakes are caught before you compile, and team code stays consistent.

**How:**

- Look at the underlined code and the Problems panel.
- The 💡 quick fix can remove an unused declaration, convert fixed-format code, or turn a check off.
- Each check can be switched on or off under *Settings → Vanthrex: Lint Rules*.
