---
layout: default
title: "PDM in one screen"
nav_order: 24
parent: "Features"
---

# PDM in one screen (2.2)
{: .no_toc }

Work with libraries, objects and members the way you do with WRKMBRPDM — option numbers, F-keys, subset — in a VS Code view.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## How to open it

- Right-click a library, a source file or a file in the Libraries view → **Work with Using PDM…**
- The list button in the Libraries view toolbar, or the quick menu (Ctrl+Alt+I).
- Type `WRKMBRPDM FILE(MYLIB/QRPGLESRC)`, `WRKOBJPDM LIB(MYLIB)`, `WRKLIBPDM LIB(APP*)` or `STRPDM` in **Run CL Command**.

## All source files at once

Type `*ALL` in *File* (or a generic name such as `Q*SRC`), use `WRKMBRPDM FILE(MYLIB/*ALL)`, or option **AM** on a library: the members of every matching source file appear in one list, with a *File* column. Every option works across files, and F6 asks which source file the new member goes in.

## Options

| Level | Options |
|---|---|
| Members | 2 Edit · 3 Copy · 4 Delete · 5 Display · 6 Print · 7 Rename · 8 Description · 13 Change text and type · 14 Compile · 15 Create module · 16 Local history · 25 Find string · 54 Compare · OB Objects built from it · SC Changes since last compile · PN Pin · GH Git history · UC Unused code · HL Hard-coded libraries |
| Objects | 4 Delete · 5 / 8 Display · 7 Rename · 11 Move · 12 Work with members · 13 Change text · 15 Duplicate · 16 Call · 18 Edit data · 34 Debug · WU Where used · LK Locks · DP Dependents |
| Libraries | 5 / 12 Work with objects · 8 Description · 13 Change text · SF Source files · AM All members · LL Add to library list · CL Set current library |

Type options on as many rows as you like and press **Enter**. Deletes are confirmed once for the whole batch; each row shows ✓ or the error in the *Status* column.

## Function keys

| Key | Action |
|---|---|
| F3 | Exit |
| F5 | Refresh |
| F6 | Create a member, source file or library |
| F9 | Undo the last delete (members) |
| F12 | Back to the previous list |
| F13 (Shift+F1) | Repeat the first option typed on every row below |
| F16 (Shift+F4) | User-defined options |
| F17 (Shift+F5) | Subset |
| F21 (Shift+F9) | Export the list to CSV |
| F23 (Shift+F11) | More options |

## User-defined options

Add your own two-letter options with F16 or the `vanthrex.pdm.userOptions` setting. Variables: `&L` library, `&F` file, `&N` name, `&T` type, `&A` attribute, `&O` object library, `&U` user, `&X` text. Text typed in *Parameters or command* is appended to the command (for example `CB` with `TGTRLS(V7R4M0)`). Built-in: CB (CRTBNDRPG), CS (CRTSQLRPGI), CC (CRTBNDCL), DF (CRTDSPF), PF (CRTPF), RS (RUNSQLSTM).

## Safety nets

- **Undo delete (F9):** before option 4 removes a member, its source is copied. F9 (or `UNDO` on the command line) puts the members of the last delete back; a copy is also kept on disk in the extension's storage.
- **Members in use** by another job (see the *In use by* column) are not deleted or renamed.
- **Failed options stay on their rows**, with the IBM i message (for example `CPF3220: …`) in the *Status* column, so you can fix and press Enter again.
- **Progress and Cancel** for batches; more than 10 changing options (copy, delete, rename, change, user options…) ask for confirmation first. Renames to a name that already exists are stopped before they run.

## See more at a glance

- **Object column:** ✓ the object in your object library is newer than the source, ⚠ the source changed after the last compile, ○ not compiled yet. Tick **Needs compile** to list only those, then type 14 and F13.
- **In use by:** the job that has the member open. Tick **In use** to list only those.
- **Type chips:** click RPGLE, CLLE… above the list to subset by type.
- **Preview:** tick *Preview* and click a member (or use ↑ / ↓) to read its first 300 lines beside the list.

## What did my source become?

- **Objects Built from This Source** — right-click a member (Libraries view or editor) or type **OB** in PDM: every program and service program compiled from the member, when it was compiled, and ⚠ when the source changed after that compile. *Compile now* is one click away.
- **Member status bar** — while you edit a member: ✓ the program it went into, ⚠ how many objects are older than your source, or "not compiled"; 🔒 shows who else has the member open. Turn it off with `vanthrex.memberStatusBar`.
- **Compile on save** — `vanthrex.compileOnSave`: `off`, `ask` or `always`; limit it to some source types with `vanthrex.compileOnSave.types`. Copy members are never compiled.
- **Find & Open Member…** (Ctrl+Alt+M) — a name or generic name, optionally with a type (`ORD* RPGLE`), in your library list or in every user library. Results follow library-list order; buttons open the source file in PDM or show the objects built from it.

## History, live job log and pins

- **Compile History** — every compile on this computer with its result; *Broken right now* shows the sources whose last compile failed, and **Recompile the broken sources** runs them again (with Cancel).
- **Show My Changes Since the Last Compile** — editor menu, member menu, PDM option **SC**: the lines changed after the last compile are highlighted, with a list to jump to them. Needs source dates (on by default).
- **Live Job Log** — right-click a job → *Live Job Log*: new messages appear every few seconds; escape messages and severity 30+ pop up with **Explain**; it stops when the job ends (or after 2 hours, or with *Stop Live Job Log*).
- **Pinned** — right-click a member, source file, library, object or IFS file → *Pin / Unpin* (or **PN** in PDM). Pins are kept per system; drag order with *Move Up / Move Down*.
