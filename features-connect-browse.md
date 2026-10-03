---
layout: default
title: "Connect & browse"
nav_order: 1
parent: "Features"
---

# Connect & browse
{: .no_toc }

Set up a connection, then browse libraries, source files, members, objects and the IFS.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Connection wizard and quick menu

**What it is:** A one-page form for host, user, sign-in method, library list, current library and SQL engine, with a **Test connection** button.

**Why it helps:** No hand-edited config files. The test tells you straight away whether SSH works and which SQL engine will be used.

**How:**

- **Add IBM i Connection** (the **+** on the *Connections* view).
- Right-click a connection → **Edit** or **Remove**.
- **Ctrl+Alt+I** opens the quick menu: dashboard, run CL, SQL scratchpad, search, edit data, disconnect.

## Libraries & Source browser

**What it is:** Your library list as a tree. Under each library are its **Source files** and members, and its **Objects** (programs, files, service programs…).

**Why it helps:** It is what PDM does, but with search, icons, descriptions and one-click open.

**How:**

- Click a member to open it, and press **Ctrl+S** to save it back to the IBM i.
- Right-click a library → **New Source File**, **Set as Current Library**, **Remove from List**.
- Right-click a source file → **New Member** (RPG and CL members start from a template that compiles as-is).
- The **search icon** (Find & Open Member) finds a member by name across the library list, with wildcards such as `ORD*`.

## IFS browser

**What it is:** Browse, open, create and delete stream files and folders.

**How:** Click **Go to IFS Directory** to jump to any path. Right-click a folder → **New File** / **New Folder**.
