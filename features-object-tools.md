---
layout: default
title: "Object tools"
nav_order: 9
parent: "Features"
---

# Object tools
{: .no_toc }

Object information, who has an object locked, compare two libraries, and modules & exports.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Object information

**What it is:** One page with everything about an object: owner, created, changed, last used and how many days it was used, size, the source member it was compiled from, journaling, last save, and every other attribute.

**Why it helps:** It replaces DSPOBJD, DSPPGM and a few queries, and the buttons take you straight to the next step.

**How:**

- Click any object in *Libraries & Source → Objects*, or right-click it → **Object Information**.
- The buttons open the source, show who has the object locked, list where it is used, edit a file's data or generate its SQL.
- From the quick menu (**Ctrl+Alt+I**) → *Object information…* and type `LIBRARY/OBJECT`.

## Who has this object locked?

**What it is:** The jobs holding a lock on any object (a file, data area, program…), with the person's name and the lock state — like WRKOBJLCK.

**How:** Right-click an object → **Who Has This Object Locked?** Click a job to see its job log, send the user a message asking them to release it, or end the job (needs *JOBCTL).

## Compare two libraries

**What it is:** Compares two libraries, for example DEV and PROD, and lists the source members and objects that are only in one of them or different. The newer side is shown.

**Why it helps:** Before a promotion you see exactly what will change, and you can open a side-by-side diff of any changed member with one click.

**How:** Right-click a library → **Compare Two Libraries…** (or the quick menu), pick the two libraries. Click a *different* member to compare its text; click an object for its information.

## Modules & exports

**What it is:** For a service program: its exported procedures and data in signature order. For a service program or ILE program: its bound modules with their source and dates. Modules whose source changed after they were compiled are highlighted.

**How:** Right-click a *SRVPGM or *PGM → **Show Modules & Exports**. Click a module to open its source.
