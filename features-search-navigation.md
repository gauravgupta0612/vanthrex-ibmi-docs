---
layout: default
title: "Search & navigation"
nav_order: 6
parent: "Features"
---

# Search & navigation
{: .no_toc }

Find objects and source, see where things are used, and navigate RPG like a modern language.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Search objects, search source, where used

**What it is and how to use it:**

- **Ctrl+Alt+O:** find objects by name or description, in your library list, one library or all user libraries. From a result you can open the source, see where it is used, edit data, call the program or copy its name.
- **Ctrl+Alt+F:** search the source code of a library or source file. Click a match to open the member at that line.
- **Where Used** (right-click any object): lists the programs that reference a file or program.
- **Open Program Source:** jumps from a program to the member it was compiled from.

**Why it helps:** Impact analysis before a change, with no printouts.

## RPG navigation

**What it is and how to use it:**

- **F12** goes to the definition, including definitions inside /COPY members.
- **Shift+F12** finds every use.
- **F2** renames. A local variable is renamed only inside its procedure, and fixed-format columns are protected.
- **Ctrl+click** on a `/COPY` or `/INCLUDE` line opens that member.
- Hovering a name shows its declaration. Hovering a BIF or opcode shows its syntax.
- Hovering a fixed-format line shows which field that column belongs to (Factor 1, Result field…).
- The Outline view lists procedures, subroutines, data structures and prototypes.
