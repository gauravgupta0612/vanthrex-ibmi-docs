---
layout: default
title: "Changelog"
nav_order: 90
---

# Changelog

## 1.2.0

**New: safer and sturdier — protection for production systems, a self-check, and errors that explain themselves**

- **Protect production systems.** Mark a connection as *Production* (every change asks first, with *Allow once* or *Allow for 15 minutes*) or *Read-only* (Vanthrex refuses every change). It covers CL commands, SQL that changes data or objects, member saves and IFS writes — Vanthrex's own work in QTEMP and its temporary files is not affected. The status bar shows a shield or a lock and turns red / amber so you always know where you are. Set it in the connection form or with **Set Protection…** on a connection.
- **Self-check.** **Self-Check (Is This System Ready?)** tests SSH and SQL round-trip times, QSH and CL, the SQL engine and Java version, your profile's CCSID (65535 is flagged), home directory, library list, IBM i release and Db2 PTF group, your special authorities, RPGUnit and the debug service — and lists which IBM i services Vanthrex uses are missing on this system and which features they affect. Every problem comes with how to fix it, and **Copy the report** makes support issues easy. It also runs quietly the first time you connect to a system and warns only about real problems (`vanthrex.selfCheck.onConnect`).
- **Errors that say what to do.** Error messages from IBM i, Db2 and SSH now end with a plain-language hint — a missing IBM i service points to the Db2 PTF group, "not authorized" points to *Check Authority*, SQL7008 suggests WITH NC or journaling, locks point to *Who Has It Locked?*, lost connections say how to reconnect — in all 8 languages.

## 1.1.0

**New: data, performance, code quality and unit tests**

- **Export table data to Excel, CSV or JSON** (right-click a file): with an optional WHERE filter; numbers stay numbers in Excel and the header row is frozen. **Export Query Result** does the same for the SQL statement under the cursor in a `.sql` editor.
- **Import a CSV or Excel file into a table** (right-click a file): columns are matched by name, a preview shows the mapping, the first rows and any values that don't fit (too long, not a number, too many decimals) before anything is written. Add to the table or replace its rows.
- **Performance monitor** (*Jobs* view toolbar, quick menu or right-click the active connection): live charts of CPU, system ASP, active jobs and temporary storage with hover values, top jobs by CPU and by disk I/O (click for the job log) and memory pools — refreshed every 5 seconds.
- **Code metrics** (right-click a source file, or a member's editor menu): lines, free vs fixed, procedures, subroutines, SQL, complexity, nesting, numbered indicators and GOTOs per member, with a grade A–D and modernization advice.
- **Generate documentation** for the open RPG or CL source as Markdown: description, parameters, files, calls, copybooks, procedures with their comments, and metrics.
- **RPGUnit tests**: generate a test member for the exported procedures of the open source (one test per procedure, with the right `aEqual` / `iEqual` / `nEqual`), and run tests from VS Code's **Testing** view — RUCRTRPG compiles, RUCALLTST runs, and each test shows as passed or failed with its message. Test members are found when you open them or with **Find RPGUnit Tests…** on a source file. Needs iRPGUnit on the IBM i.
- All new screens are translated into the 7 languages.

## 1.0.0

**Vanthrex for IBM i 1.0 — stable release**

1.0 brings together everything since 0.1: editing and compiling with SEU habits kept, SQL and data tools, debugging, the AI assistant, insights, system tools, the *Work with…* screens and 8 languages. New in 1.0:

- **Storage & cleanup advisor** (quick menu, or right-click a library): libraries and objects by size, objects not used for 90–730 days, files with many deleted rows (one-click RGZPFM), saved journal receivers older than 30 days (DLTJRNRCV), and spooled files older than 30 days by user (delete them in one go) — with an estimate of the space you can free. **IFS folders by size** does the same for the IFS.
- **Live alerts** (turn on in the *Jobs* view toolbar → *Live Alerts*, or `vanthrex.alerts.enabled`): a VS Code notification when one of your jobs — or anyone's, with `vanthrex.alerts.scope: all` — waits for a reply (MSGW), an inquiry arrives on QSYSOPR (reply straight from the notification), a batch job ends abnormally, or the system ASP passes 85%. A bell in the status bar counts what is waiting.
- **Message files** (right-click a `*MSGF`): every message description with its text, help and severity; add (with the next free ID proposed), change, copy as ADDMSGD or remove.
- **Field finder**: find every file, table and view that has a field — by name, wildcard or description — see where the same field is defined with different types or lengths, and jump to the programs using each file.
- **Object promotion (DEV → TEST → PROD)** (right-click objects or a library): pick objects, compare them with the target first (new, newer in source, **newer in target**, physical files that carry data), then copy them with SAVOBJ / RSTOBJ after an automatic backup of the objects being replaced. Every promotion is recorded in a **promotion log**, from which you can undo it.
- All new screens are translated into the 7 languages added in 0.10.

## 0.11.0

**New: the IBM i "Work with" screens, in VS Code**

Open them all from **IBM i: Work with…** (quick menu, the *Jobs* view toolbar, or right-click the active connection). Every list can be filtered, and clicking a row shows its options; every command is shown before it runs.

- **Work management:** subsystems (start, end, the jobs in each — WRKSBS), job queues (hold, release, clear, and release / hold / prioritise / end the waiting jobs — WRKJOBQ), output queues and the spooled files on any of them (open, hold, release, move, delete — WRKOUTQ), and the job scheduler (add, hold, release, remove entries — WRKJOBSCDE).
- **Users & security:** user profiles with filters (non-IBM, disabled, special authorities, groups) — enable, disable, expire the password, see a user's active jobs and owned objects (WRKUSRPRF); all system values with the important ones explained (WRKSYSVAL, read-only); and the security audit journal QAUDJRN — authority failures, invalid passwords, profile and system value changes, deleted objects… — for a time range and user.
- **Save / restore:** save files in a library and what is inside them, SAVLIB / SAVOBJ to a save file (target release, compression, run now or in batch), RSTLIB / RSTOBJ (also into another library), and download / upload a save file between the IBM i and your PC. Right-click a library or a save file.
- **Network & services:** TCP/IP connections with the job and user behind each (end a connection), listening ports, the TCP/IP servers (SSH, host servers, DDM, FTP, Telnet, HTTP admin, NetServer, SMTP) with start / end, and IP interfaces and routes.
- All of it is translated into the 7 languages added in 0.10.

## 0.10.0

**New: Vanthrex speaks your language**

- The whole user interface — commands, menus, views, settings, the Getting Started walkthrough, messages, prompts and report titles — is now available in **French, Spanish, German, Italian, Portuguese (Brazil), Japanese and Simplified Chinese**, in addition to English.
- Vanthrex follows the VS Code display language: **Ctrl+Shift+P → Configure Display Language**, pick the language (install its language pack if asked) and restart VS Code.
- IBM i names stay as they are on the system — commands (CHGDTAARA, GRTOBJAUT…), object types (*FILE, *PGM…), message IDs and SQL — and the translations use IBM's own IBM i terminology for each language.

## 0.9.0

**New: system tools**

- **Journal Explorer: Who Changed This Table?** (right-click a file): row changes from the journal for a time range — added, updated, deleted, by which user, program and job — with before/after images of updates, a "who changed it" summary and the history of a single row. Offers `STRJRNPF` when the file isn't journaled.
- **Check Authority (Can a User Use This?)** (right-click any object): resolves a user's authority in IBM i order (*ALLOBJ → own → groups → authorization list → *PUBLIC), checks the library too, explains where the authority comes from and what is missing, and offers the `GRTOBJAUT` fix.
- **Data queues & data areas** (right-click a `*DTAQ` / `*DTAARA`): peek at data queue entries without removing them, send a test entry, clear the queue; view a data area and change its value with type, length and decimal checks.
- **PTF & System Health** (quick menu, or right-click the active connection): PTF groups compared with IBM's latest levels, PTFs waiting for an IPL, system ASP use, certificates expiring within 60 days, and user profiles with default or expiring passwords — worst first, with what to do.

## 0.8.0

**New: insights for faster troubleshooting**

- **Index Advisor** (right-click a library, or the quick menu): every index Db2 for i itself recommended while your application ran (`QSYS2.SYSIXADV`) across your libraries, most requested first, with the cost of the most expensive query. Click a suggestion to create the index — a name is proposed and the SQL is shown before it runs. *Show Queries Running Now* lists the active SQL on the system.
- **Compare table data (DEV ↔ PROD)** (right-click a file): compares the rows of the same table in two libraries by key (primary key pre-selected) — exact counts of rows only in one copy and changed rows, a field-by-field list of what changed (`BALANCE: 10.00 → 12.50`), and CSV export.
- **Message help everywhere**: hover any message ID (CPF9801, MCH1211, RNQ0102, SQL0204…) in any editor — job logs, compile listings, spooled files, comments — to see IBM's text, severity, plain-language advice and the full help text. **Explain Message ID…** does the same on demand.
- **Job log analyzer** (right-click a job → *Analyze Job Log*): groups the errors, highlights the most likely root cause (not the generic CPF9999 function check) and says what to do.

## 0.7.1

**New: SQL editor with results, right where you are**

- **Run SQL Query…** on any library, source file, member or object in the *Libraries & Source* view (right-click), in the call graph (**Run SQL…** button, or click an object), on *Object information*, *Who calls each exported procedure?* and in the quick menu.
- It opens an SQL editor already filled with a useful query for what you clicked — first 100 rows, row count and columns of a file; program information, bound modules, exports and the programs bound to a service program; objects, tables and source members of a library; lock holders; and more. Pick another ready-made query from the list or write your own.
- **▶ Run** (or Ctrl+Enter) shows the data underneath: sort by clicking a column, filter rows, copy as CSV, or open the query in an SQL scratchpad. Destructive statements still ask first.

## 0.7.0

**New: Who calls each exported procedure?**

- Right-click a service program → **Who Calls Each Exported Procedure?…** (also on the object information page, *Modules & Exports* and the call graph). Vanthrex finds the programs bound to it (QSYS2.BOUND_SRVPGM_INFO, or the DSPPGMREF cross-reference), reads their RPG and CL source — with the prototypes in their /COPY members — and lists, for every exported procedure, each program, source line and statement that calls it.
- Prototypes are followed: `EXTPROC('SYMBOL')`, `EXTPROC(*DCLCASE)`, fixed-form `PR` specs (long names too), `CALLB`, `%PADDR` and CL `CALLPRC`.
- Exported procedures nobody calls in the analysed libraries are marked, as are calls matched by name only because a /COPY member could not be read. Click a call to open the source at that line.

**New: dynamic calls in the call graph**

- **Find dynamic calls** scans the source of the programs in the graph for calls whose target is only known at run time — `CALL` with a variable in RPG, prototypes with `EXTPGM(variable)` / `EXTPROC(variable)`, CL `CALL PGM(&VAR)` — and shows them as dashed red nodes. Click one to open the call. DSPPGMREF cannot see these calls, so the graph now tells you where it is blind.

## 0.6.1

- **Stable release:** Vanthrex for IBM i is no longer marked as *Preview* on the VS Code Marketplace.
- Releases are published to the Marketplace automatically when a version tag is pushed (needs the `VSCE_PAT` repository secret).

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
