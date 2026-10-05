---
layout: default
title: "Changelog"
nav_order: 90
---

# Changelog

## 0.6.0

**New: AI assistant for IBM i (`@vanthrex`)**

- Type **@vanthrex** in the VS Code chat (GitHub Copilot Chat or any chat model) and ask about IBM i in plain language. Commands: `/explain`, `/document`, `/review`, `/modernize` (fixed format → modern **FREE RPG), `/test` (RPGUnit tests), `/fix` (explain and fix compile errors), `/sql` (Db2 for i SQL written against your real tables and columns) and `/object LIB/NAME *TYPE`.
- The assistant knows the connected system (library list, IBM i release) and can look things up: object descriptions, table columns and indexes, source members, object search, system status and read-only queries.
- **Safe by design:** it only reads. Queries must be a single SELECT / WITH / VALUES (data-change statements and functions with side effects such as QCMDEXC are refused), and Vanthrex asks before every query and before reading an IFS file.
- Right-click in a source → **Vanthrex AI** (Explain, Document, Review, Modernize, Unit tests, Fix compile errors, Write SQL); the 💡 on an IBM i compile error offers **Ask AI to explain and fix**; right-click an object → **AI: Explain This Object**.
- The same tools work in **Copilot agent mode**: `#ibmiQuery`, `#ibmiSource`, `#ibmiObject`, `#ibmiSearch`, `#ibmiStatus`.
- Settings: `vanthrex.ai.enabled`, `vanthrex.ai.useTools`, `vanthrex.ai.allowQueries`, `vanthrex.ai.confirmQueries`, `vanthrex.ai.maxSourceChars`.

**New: Git for IBM i source**

- **Git: Export Source to a Git Repository** (right-click a library or source file): saves every member as `library/sourcefile/member.type`, then offers to create the repository, make the first commit and publish it (GitHub, GitLab, Azure DevOps…).
- **Git: Get Changes from IBM i** brings in only the members changed on the system since the last sync; **Git: Upload Changed Files to IBM i** sends only the files you changed — to their own libraries or to another one (for example your development library). Files changed on both sides are flagged, never silently overwritten.
- **Git: History of This Member**: every committed version of the member you are editing — compare with the IBM i copy, compare with the previous version, open it, or restore it into the editor.
- **Git: Commit & Push** with the author from your Git configuration or from `vanthrex.git.authorName` / `vanthrex.git.authorEmail`.

**New: call graph & impact analysis**

- **Call Graph** (right-click a program, service program or file): an interactive diagram of who calls the object (callers, the impact of a change) and what it uses (programs, service programs, files with input/output/update usage), several levels deep. Pan, zoom, change depth, hide files, click any object for its actions, and **Copy as Mermaid** for docs and pull requests.
- **Impact Analysis (Who Uses This?)**: the callers view directly, with a count of the programs and libraries affected.

**New: several systems at once**

- Connect to more than one IBM i (for example DEV and PROD) and switch instantly with **Switch IBM i System** (quick menu, status bar or the Connections view). Other systems stay connected in the background.
- A member or IFS file is always saved to the system it was opened from — saving while another system is active is refused with a clear message.

**New: SQL performance — Explain**

- **Explain SQL (Performance)** in a SQL editor (also on the editor title): runs the query under a database monitor and summarises the access plan — table scans and why, indexes used, temporary indexes, sorts — with tips, the optimizer's **advised indexes** and the index advisor history, plus a ready-to-review `CREATE INDEX` statement.

**Better: fixed → free conversion**

- **Convert Fixed Format to Free** now converts **H, F, D and P specs** too: `ctl-opt`, `dcl-f` (usage, keyed, devices, program-described files), `dcl-s`, `dcl-c`, `dcl-ds` / `end-ds` (overlay → `pos`, externally described, LIKEDS), `dcl-pr` / `dcl-pi` with parameters, `dcl-proc` / `end-proc`, long names, continued keywords and literals. Compile-time data is left untouched and long statements are wrapped at column 80.

**Other**

- Requires VS Code 1.95 or later.

## 0.5.0

**New: IBM i debugger**

- **Debug Program** (Ctrl+Alt+G, the 🐞 button on a program, or the editor title of an RPG/CL source): runs the program in a batch job under the IBM i debugger and opens a full VS Code debug session — breakpoints, step over/into/out, variables, watch and call stack. Parameters for the CALL are remembered per program.
- Uses IBM's free **IBM i Debug** extension as the debug client and the **IBM i Debug Service** on the server; Vanthrex installs the client on request, reads the service's port and certificate locations, downloads and trusts the certificate, and starts the session for you.
- **Debugger Setup Check**: one page that checks the client, the Debug Service (installed, running, certificate) and this PC's certificate, with buttons to fix each item — including **Start Debug Service**.
- Settings: `vanthrex.debug.port`, `vanthrex.debug.ignoreCertificateErrors`, `vanthrex.debug.updateProductionFiles`, `vanthrex.debug.trace`.

## 0.4.0

**Fixes**

- **Members now always open.** With the Mapepire SQL engine, opening a member could fail with *"The editor could not be opened due to an unexpected error"* (log: *Result set was null*). Statements that return no rows are now handled correctly, and if reading with source dates ever fails the member opens without dates instead of failing.
- **Lock information works on all releases**: the lock check used a column name (`MEMBER_NAME`) that `QSYS2.OBJECT_LOCK_INFO` does not have.

**New: object & job tools**

- **Object information** page: owner, created/changed/last used, days used, size, source member, journaling and every other attribute — click any object in the Libraries view. Buttons to open the source, see locks, where used, edit data and generate SQL.
- **Who has this object locked?** for any object, with job log, *Ask to release* and *End job* per lock holder.
- **Compare two libraries** (for example DEV and PROD): objects and source members that are only in one library or different, with a side-by-side diff of changed members.
- **Modules & exports** of a service program or ILE program, with modules whose source changed after they were compiled highlighted.

**New: SQL power tools**

- **Generate SQL (DDL)** for any table, view, index, procedure or function (`QSYS2.GENERATE_SQL`).
- **Run SQL Script** (Ctrl+Shift+Enter): runs every statement in the file and shows each result, row count or error. Stops at the first error unless `vanthrex.sql.scriptStopOnError` is off.
- **SQL history** and **saved queries**: rerun, open, insert or copy a statement; star the ones you use often.

**New: procedure & copybook tools (RPG)**

- **Generate prototype from procedure**: builds the DCL-PR from a procedure's DCL-PI, ready for your prototype copybook.
- **Extract to procedure**: moves selected free-form lines into a new procedure and calls it — refused when that would change behaviour (local variables, early exits, unbalanced blocks).
- **Check /COPY usage**: lists each copybook with the declarations the source actually uses, and comments out unused ones on request.

## 0.3.1

- **Documentation site**: full user documentation is now online at https://gauravgupta0612.github.io/vanthrex-ibmi-docs/ (installation, IBM i setup, every feature, commands, settings, troubleshooting and FAQ).
- New command **Vanthrex: Open Documentation**, also in the quick menu (Ctrl+Alt+I) and in the `…` menu of the *Connections* view.
- The Marketplace page links to the documentation.
- Release workflow fix: GitHub Packages publishing no longer runs the Marketplace publish script.

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
