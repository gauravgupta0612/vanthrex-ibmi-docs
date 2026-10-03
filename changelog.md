---
layout: default
title: "Changelog"
nav_order: 90
---

# Changelog

## 0.3.0

- **New name: Vanthrex for IBM i** (formerly *Silverlake*), first release on the VS Code Marketplace. Settings now start with `vanthrex.`; connections are set up again after installing.
- **SEU-style source dates**: every member line shows its change date (and optionally its sequence number). Saving keeps the dates of lines you did not touch; changed lines get today's date. Ctrl+Alt+D cycles the display.
- **Highlight lines changed since…** a date (7 / 30 / 90 days or any date), with a list to jump between them.
- **Lock information in the editor**: a banner shows who has the member open (name, user, job, lock state), with *Ask to release* (break message), *Notify me when free* and *End their job*.
- **Edit conflict protection**: warns before saving over a member that someone changed after you opened it (with *Compare first*), or that is locked by another job.
- **F4 prompter** for fixed-format RPG (H, F, D, P, C specs) and DDS: edit the columns in a labelled form.
- **CL command prompter**: F4 on a CL command (or *Prompt and Run CL Command*) builds a form from the command's real definition on the IBM i.
- **Member list**: last change date in the tree, sort by name or date, filter by "changed in the last N days".
- Safer member saves: lines are staged in QTEMP and the member is replaced in one step, with automatic restore if the replace fails.
- Releases are also published to **GitHub Packages**.

## 0.2.0

- **System dashboard**: CPU, ASP, jobs, memory, top jobs, QSYSOPR messages and PTF groups, refreshing automatically.
- **Active Jobs** view: filter by me, user, subsystem or all; job log, hold, release, end.
- **Messages** view: QSYSOPR and your own queue, inquiry messages first, reply and remove, send messages.
- **Table data editor**: filter, page, edit, insert and delete rows, with type validation before writing.
- **Object search** (Ctrl+Alt+O), **source code search** (Ctrl+Alt+F), **Where used**, **Open program source**.
- **RPG navigation**: go to definition (including /COPY members), references, scoped rename, occurrence highlight, /COPY links, declaration hover.
- **SQL autocomplete and hover** for tables, views and columns from the Db2 for i catalog.
- **Local history**: versions of every member and IFS file you open or save; compare, restore, compare with the IBM i copy, compare two members.
- **RPG code checks** with quick fixes and per-rule switches.
- The extension now reports start-up problems instead of failing silently.

## 0.1.0 (first release)

- Guided connection form with **Test connection**; passwords kept in the VS Code secret store.
- Status bar menu (Ctrl+Alt+I) for quick actions.
- Libraries & Source browser: source files, members, objects; add/remove libraries, set the current library.
- Find a member by name pattern across the library list.
- Edit source members and IFS files in place (UTF-8 transfer through CCSID 1208).
- One-key compile with configurable actions and inline errors from EVFEVENT.
- Db2 for i SQL: Mapepire over SSH (no server install, needs Java), Mapepire daemon or db2util; results grid with sort, filter and CSV export.
- CL command runner with history.
- Spooled file viewer: open, save, delete.
- RPG: syntax highlighting (free and fixed), outline, hovers for BIFs/opcodes, fixed-format column hints, `%` completion, snippets, fixed C-spec → free conversion.
- CL and DDS syntax highlighting and snippets.


Full release history: [GitHub Releases](https://github.com/gauravgupta0612/silverlake-ibmi/releases).
