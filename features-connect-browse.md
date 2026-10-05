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

## Several systems at once

**What it is:** Stay connected to several IBM i systems — for example DEV, TEST and PROD — and switch between them instantly. New in 0.6.

**Why it helps:** Compare, check production or answer an operator message without disconnecting from your development system.

**How:**

- Click another connection: it connects and becomes the **active** system; the others stay connected in the background (a blue icon in the *Connections* view, and `+1` next to the system name in the status bar).
- Switch with **Switch IBM i System** — the ⇄ button on the *Connections* view, the quick menu (**Ctrl+Alt+I**), or click a background connection. Switching needs no new sign-on.
- The views (libraries, IFS, jobs, messages, spooled files) and commands always work on the active system.
- **Safe saving:** a member or IFS file is always saved to the system it was opened from. If another system is active, the save is refused with a message telling you to switch back.
- Disconnect one system with the ✕ next to it, or all with **Disconnect All Systems**.
- Prefer one system at a time? Turn off `vanthrex.connections.keepOthersOpen`.

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
