---
layout: default
title: "Changelog"
nav_order: 90
---

# Changelog

## 2.5.0 (not released yet)

**AI with your data protected**

Everything sent to the AI now goes through one guard, and nothing the AI does can change the IBM i.

- **Secrets never leave your computer**: passwords (CL `PASSWORD(…)` and `CHGVAR` of a password variable, `pwd = …`, `DB_PASSWORD=…`, `password: …`, ODBC / JDBC connection strings, FTP `PASS` and `USER name password`, SQL `USING '…'` and encryption passwords, constants named like a password), API keys, tokens (GitHub, GitLab, npm, AWS, Slack, Google, JWT, Basic and Bearer), private keys and credentials in URLs are replaced by placeholders (xxxx1, xxxx2…) before anything is sent — in the source, query results, job logs, tool results and the chat history. The AI keeps the placeholders; the **real values are put back only on your computer**, in the answer you read and in the code you apply. Special values (`*NONE`, `*USRPRF`) and variables (`&PWD`, `:host`) are left alone.
- **Personal data and internal names hidden**: e-mail addresses, payment card numbers (Luhn-checked), IBANs (checksum-checked), US social security numbers, international phone numbers, IP addresses, the host names of your connections, and your own list of words (customer names, project code names) — each can be switched in the settings.
- **Sensitive columns masked**: query results the AI reads show `xxxx` for columns such as PASSWORD, EMAIL, PHONE, IBAN, CARD, SALARY, BIRTH (your own list in `vanthrex.ai.sensitiveColumns`).
- **Production stays private**: on protected connections the AI reads source and catalog facts (object descriptions, columns, members, indexes, command definitions, message help) but **cannot run queries of its own, read spooled files or non-source IFS files** (`vanthrex.ai.productionData`: metadata / full / none); `vanthrex.ai.otherSystemsData` does the same for the other systems.
- **Safer AI queries**: a query the AI writes may not call functions that reach other servers or read files, spooled output, journals, data queues or data areas (HTTP_GET, IFS_READ, SPOOLED_FILE_DATA, DISPLAY_JOURNAL, QCMDEXC…); a sensitive column renamed with AS or used in an expression is refused; unqualified tables are refused when a hidden library is in the library list; card numbers stored as numbers are hidden too.
- **Source means source**: the AI reads members of source files only (never members of data files), refuses /QSYS.LIB paths and key, certificate and credential files.
- **No way out through links**: real values are put back only for placeholders sent in that request, and never inside a link or URL of an answer (so injected text cannot make the answer send a secret anywhere). Values shown in an answer are hidden again when the chat history is sent back.
- **Libraries never shared**: `vanthrex.ai.deniedLibraries` (wildcards like `PAY*`) — sources, objects, queries and authorities in them are refused, even when named inside a string.
- **No surprise reads**: IFS files that look like keys, credentials or system files are refused; every query still asks first and is read-only.
- **Prompt-injection guard**: source, rows, job logs and messages are sent as framed data the model is told never to obey.
- **Audit trail and transparency**: after an answer you see how many values were hidden; **AI: Privacy and Security** shows the settings, what was hidden this session and every request (time, system, feature, size — never the content), also kept in the *Vanthrex AI Audit* output and a file; **AI: Preview What the AI Sees** shows the open file side by side with what would be sent.

**New AI features**

- **AI: Change the Selected Code…** (Ctrl+Alt+E): say what to change ("add MONITOR around the I/O", "rename x to customerNumber", "convert to free form"); the proposal opens as a **diff** and is applied only when you click *Apply* (one Ctrl+Z undoes it), never if the source changed meanwhile.
- **✨ Explain · Document · Tests** above every RPG procedure and subroutine (`vanthrex.ai.codeLens`).
- **/tune — Make This SQL Faster**: reads each table's size, its indexes (and how often queries used them) and the optimizer's index advice, then rewrites the statement and writes the CREATE INDEX worth creating.
- **/sqlio — Convert File I/O to Embedded SQL**: CHAIN, READ, SETLL, WRITE, UPDATE… to cursors and SELECT INTO, with SQLSTATE checks and the locking notes.
- **/changes — Review My Changes**: only the lines you changed are sent and reviewed — against Git HEAD for local files, the copy on the IBM i for unsaved changes, or the latest change day of the source dates for members.
- **/cl — Write CL from a description**, using the real command definitions of your system.
- **/data — Test data for a table**: realistic invented INSERTs that respect types, keys and foreign keys — only the table's structure is read, never its rows.
- **/health — Is the system healthy?**: CPU, storage, jobs waiting for a reply, top CPU jobs, QSYSOPR, subsystems — what needs attention first and the next step.
- **/security — Review authorities** of an object or a library: *PUBLIC exposure, owners, adopted authority, with the GRTOBJAUT / RVKOBJAUT / CHGOBJOWN to fix each finding.
- **/spool — Explain a spooled file** (right-click it): a dump, a job log, a compile listing or a report in plain words.
- **Four more tools for the AI and Copilot agent mode**: `#ibmiMessage` (IBM message help), `#ibmiMembers` (members of a source file), `#ibmiCommand` (CL command definitions), `#ibmiIndexes` (table size, indexes and index advice) — all read-only and through the same guard.

## 2.4.0

**Local development (like Code for IBM i, with less setup)**

- **Deploy Changes to IBM i (IFS)** (right-click in the Explorer, quick menu): keep your source in a local Git folder and upload only new and changed files to an IFS folder of their own (`${home}/builds/<folder>` by default, `vanthrex.deploy.directory`). Missing folders are created, files are tagged CCSID 1208 so the compilers read them right, `.git`, `node_modules`, `.vscode`, keys and logs are never sent (`vanthrex.deploy.ignore`). **Deploy All Files** sends everything again; `vanthrex.deploy.onSave` uploads each file as you save it. A protected system asks once for the whole deploy.
- **Compile Local File on IBM i** (editor title button, right-click, and the normal Compile key on a local file): deploys the file (and every changed copybook, so `/COPY` and `/INCLUDE` see your latest version), compiles it from the stream file with your compile actions, and shows the errors **on the local file** — and on the local copybook when the error is in one.
- **Build Project on IBM i**: runs your build command (`makei build` for Bob / IBM i Project Explorer, `gmake`, your own script) in PASE in the deploy folder, with the open-source tools on the PATH and `CURLIB` / `LIBL` from the connection. Output in the *Vanthrex Build* panel, the message IDs it found and the exit code in the summary.
- **PASE terminal** (Ctrl+Alt+P, connection right-click, the terminal **+** menu as *IBM i (PASE)*, *Open PASE Terminal Here* on IFS folders): a real interactive shell on the IBM i in VS Code's terminal panel, over the connection you already have — no second sign-on, `/QOpenSys/pkgs/bin` first on the PATH, resizes with the panel.

**SQL and Db2 for i**

- **IBM i notebooks** (`.vxnb`, *New IBM i Notebook*): SQL, CL and PASE shell cells with Markdown notes in one file — a runbook, a health check, an investigation you can share. Results are tables (and stay out of the file), CL cells show every message and printed output, shell cells their output; **Export Notebook to Markdown** for a ticket or a wiki.
- **Charts from SQL**: put `-- chart: bar|line|pie Title` above a query in a notebook and the result is drawn (labels from the first column, up to four number columns); `-- rows: 5000` reads more rows.
- **SQL Error Log** (*Who Gets Which SQL Error?*): the SQL Error Logging Facility (SELF) shows which programs and jobs get which SQLCODE, how often and with which statement — most frequent first, each one explained in a click. **Turn SQL Error Logging On or Off…** for the whole system (`*ERR`, `*ALL`, chosen codes, `*NONE`) or only your session.
- **Browse Schema (SQL Objects)** (right-click a library, quick menu): every table, view, index, procedure, function, trigger, sequence and global variable of a schema with long and system names, counts by kind and a filter; click one for its **CREATE statement**, its data, what depends on it, or to call it. Kinds a release does not have are reported and the rest still shows.
- **Call Stored Procedure…**: finds the procedure, asks for each parameter with its SQL type (numbers and lengths checked as you type, `NULL`, empty = default), remembers your last values, and shows the **OUT / INOUT values** and the **result set** — OUT values come back through global variables in QTEMP, no host program needed.

**Editor**

- **Folding** for RPG (free and fixed form: procedures, DS / PR / PI, IF, DO, FOR, SELECT, MONITOR, BEGSR, P-specs) and CL (DO / ENDDO including `THEN(DO)`, SELECT, SUBR).
- **Parameter hints** while typing an RPG call: the parameters of the procedure or prototype (free and fixed D-specs) with the current one highlighted, and of the common built-in functions (%SUBST, %SCAN, %DEC, %DATE, %SPLIT…).
- **Format Document** for fully free RPG (`**FREE`): re-indents by block (ELSE / WHEN / ON-ERROR one level back, continuation lines keep their offset, compile-time data untouched); `vanthrex.editor.rpgIndent`.
- **Fixed-format fields**: the status bar shows the RPG or DDS field under the cursor (spec, name, columns); **Ctrl+Alt+]** / **Ctrl+Alt+[** jump to the next / previous field, *Fields of This Line…* lists every field with its value.
- **CL language support**: an outline (variables with type and length, files, labels, subroutines), Go to Definition for `&variables`, `GOTO` labels and `CALLSUBR`, Find All References, highlights, and hovers with the declaration.

**CL and RPG editing**

- **CL command help from your own system**: hover a command in a CL source for what it does and every parameter (keyword, prompt, default, allowed values, required ones marked); while typing, the keywords not used yet are offered (required first, with their default filled in) and inside `KWD(` its allowed values. Read from the command definitions on the connected system (the same ones F4 uses), so your own commands work too; `vanthrex.editor.clCommandHelp`.
- **Quick fixes for compile errors**: on *RNF7030 name not defined* the light bulb offers **Declare it here** (a `dcl-s` in the procedure that uses it, after its interface) or **Declare it globally**, with the type picked from a list; fixed-format sources get a D-spec in the right columns. Unused declarations (*RNF7031*) are now shown faded, with **Remove unused declaration**.
- **Command definition sources (.cmd)**: problems CRTCMD would reject are underlined as you type (duplicate keywords, a TYPE pointing to no QUAL/ELEM label, MIN larger than MAX, DFT on a required parameter, RSTD(*YES) without values, DEP on an unknown parameter, missing prompts), and **Preview Command Prompt (F4) from Source** shows the prompt screen before compiling — try values and copy the command they build.
- **Retrieve CL Source (RTVCLSRC)** on a CL program: the source of a program created with ALWRTVSRC(*YES) opens in an editor, no source file needed.

**SQL and code generation**

- **Run / Explain / RPG code links** above every statement of an SQL file (`vanthrex.editor.sqlCodeLens`): work through a script one statement at a time without selecting.
- **Generate RPG for This Query**: a cursor loop with a multi-row FETCH and a data structure whose subfields have the real column types (read from the system), null indicators when a column can be null.
- **Generate RPG from a JSON Sample**: select JSON, copy it, or right-click a .json file — qualified templates for nested objects, `dim()` arrays with their count fields, names made RPG-valid (with the JSON name as a comment), and the DATA-INTO / DATA-GEN statements for YAJL.
- **Find a Value in Table Data…** (right-click a file): every row where any column holds the value — text anywhere in text columns (any case), numbers in number columns, dates by their start — with the column it was found in.
- **Copy Rows as SQL INSERT Script…** (right-click a file): the rows you choose with a WHERE condition as `INSERT … WITH NC` statements, to load a test system or keep a data fix.
- **My SQL Job**: the job that runs Vanthrex's SQL, F4 and command line — its library list and its job log (newest first, message IDs explained in a click).

**IFS and work management**

- **Compare Folder with IFS…**: a local folder against an IFS folder — newer on the PC, newer in the IFS, different, only on one side — with a diff, upload or download for each file.
- **Extract Here…** (.zip, .jar, .tar, .tar.gz, .gz) and **Compress (zip / tar)…** on the IFS, with `unzip` / `zip` when installed and `jar` otherwise.
- **Copy To…** and **Move or Rename…** for IFS files and folders (whole folders, CCSID tags and permissions kept, one question before replacing).
- **Work with Job Descriptions** (WRKJOBD): user, job queue, initial library list and logging of every job description of a library; change the library list or the job queue (CHGJOBD after a confirmation), or use the library list for your connection.

**IFS**

- **Upload Files or a Folder Here…** and **drag and drop** from the Explorer or the desktop onto the IFS view: whole folder trees, parents created, `.git` skipped, one question before replacing, one progress bar.
- **Download to This PC…** on any IFS file or folder (folders with everything in them).

## 2.3.0

**Create from anywhere**

- **Create Library…** (Libraries view toolbar, quick menu, System Tracker, F6 in PDM): name, text, *TEST or *PROD, and in the same step add it to your library list, make it your current library and create the usual source files (QRPGLESRC, QCLLESRC, QDDSSRC, QSQLSRC, QCPYSRC, QSRVSRC, QCMDSRC) — then open it in PDM.
- **Create IFS Folder or File…** (IFS view toolbar, right-click a folder, quick menu, System Tracker): any path, missing parent folders created, new files tagged UTF-8 (CCSID 1208) and opened in the editor, optional permissions (chmod).

**More stable connections**

- **Automatic reconnect:** when the connection drops (network, VPN, laptop sleep), Vanthrex reconnects by itself with your saved sign-on — 5 attempts over about 2 minutes, shown in the status bar — and makes that system active again (`vanthrex.connections.autoReconnect`). Disconnecting on purpose never reconnects.
- **Connection health:** every minute a tiny query checks that the active system still answers; a slow answer shows its response time in the status bar, and a system that stops answering is reconnected even when SSH did not notice (`vanthrex.connections.healthCheckSeconds`, *Check Connection Health*, *Reconnect Now*).
- **No lost saves:** if a member or IFS file cannot be saved because the connection is gone, the change is kept on this computer and offered for saving as soon as the system is back (*Save Now*, *Show*, *Discard*; *Changes Kept While Offline…*).
- **Editors come back:** member and IFS tabs that could not be read while offline (for example after restarting VS Code) reopen by themselves once you are connected.
- **Disconnect asks first** when members or IFS files have unsaved changes (*Save and Disconnect* / *Disconnect Anyway*).

**Call, sign-on and notes**

- **Call Program (Typed Parameters)…** (right-click a program, PDM option 16): reads the parameters from the program's source — free-form `dcl-pi`, fixed `D … PI`, `*ENTRY PLIST` or a CL `PGM PARM(…)` — asks for each value with its type, checks it as you type, and builds a CALL the program receives exactly: packed, zoned and integer values become the right hex or zoned literals instead of the packed(15,5) that a plain CALL passes, and long character parameters are padded. Run it, submit it to batch or copy the command; your last values are remembered.
- **Who Is Signed On** (Jobs view toolbar, quick menu, System Tracker): every 5250 session and the server connections per user (ODBC/JDBC, file server, remote command, SSH…); for a session: details, job log, a break message or ending it (asked first); **Message everyone signed on**.
- **Member notes:** right-click a line → *Add Note to This Line*; notes show at the end of the line and as a *📝 N notes* lens at the top, follow the line when code moves, and are listed with *All Member Notes…*. Share them with your team through an IFS file (`vanthrex.notes.sharedFile`).

**Layout, includes, signatures and failed jobs**

- **Data Structure Layout** (right-click in an RPG source): every subfield of the data structure at the cursor with its type, from and to positions and length in bytes — free and fixed form, POS, OVERLAY (also `*NEXT`), DIM, LIKE and LIKEDS within the source, and EXTNAME / externally described structures with their fields read from the database. Hover a subfield definition to see its positions; copy the layout as a Markdown table.
- **Show Source with /COPY Expanded** (right-click in an RPG source): a read-only copy of the source with every /COPY and /INCLUDE merged in place (nested ones too, each marked with where it starts and ends), so you can read or search the whole program the way the compiler sees it.
- **Check Service Program Signatures** (right-click a service program): every program and service program bound to it, with the ones that would fail with a signature violation at the next call shown first, and a one-click re-bind (UPDPGM / UPDSRVPGM with MODULE(*NONE), asked first) — one object or all of them.
- **Failed Jobs** (Jobs view toolbar, quick menu, System Tracker): jobs that ended abnormally in the last hour, day or week from the history log, with the meaning of each end code, which job names fail most, and their job log one click away.

**Green screen**

- **Open 5250 Session** (right-click the active connection, the Connections toolbar or the quick menu): opens a real 5250 session on the system you work with — in IBM i Access Client Solutions when it is installed (found automatically, or `vanthrex.5250.acsPath`), in tn5250 inside a VS Code terminal, or with your own emulator (`vanthrex.5250.command` with `${host}`, `${user}`, `${device}`). Device name, TLS and port can be set.
- **Command line (5250 style)** (Ctrl+Alt+K): `===>` like on a green screen, with F4 prompt, F9 / ↑ retrieve, F12 clear and the history of your commands. Every command shows its full messages (completion, diagnostic, escape — click a message ID for IBM's help), display commands such as DSPLIBL, DSPFD, DSPOBJAUT or DSPJOB show their printed output right there (OUTPUT(*PRINT) is added for you and the spooled file removed again), and interactive commands open the Vanthrex screen that does the same: WRKACTJOB, WRKOBJLCK, DSPJOBLOG, WRKJOB, DSPMSG / WRKMSGQ, WRKSYSVAL, WRKUSRPRF, WRKOUTQ, WRKJOBQ, WRKSBS, WRKJOBSCDE, NETSTAT, DSPOBJD, DSPFD, STRSQL, STRSEU, WRKSAVF and the PDM commands. Commands that need a display (STRSDA, SIGNOFF…) offer to open a 5250 session. *Run CL Command* opens the same screens for interactive commands.
- **Work with Active Jobs** (Jobs view toolbar, connection menu, System Tracker, or WRKACTJOB on the command line): jobs grouped by subsystem with the familiar option field — 3 hold, 4 end (controlled or immediately, asked once for all), 5 work with, 6 release, 7 display and answer the message a MSGW job waits for, 8 spooled files, 10 job log, 11 call stack, L live job log — F5 refresh, F10 restart statistics, F11 other columns (threads, temporary storage, CPU time, disk I/O, pool, priority), filters by subsystem, user, job and status, position to, and refresh every 5 to 60 seconds. MSGW jobs are shown in red, LCKW in orange.

**AI-powered development** (with GitHub Copilot Chat or another VS Code chat model, through `@vanthrex`)

- **Explain compile errors** (`/errors`, *AI: Explain Compile Errors*, the light bulb on an error, or *Explain with AI* when a compile fails): every error explained in plain words with the source lines around it and IBM's own help text for the message, errors with the same cause grouped, and the smallest fix for each — without rewriting the source.
- **Generate RPG documentation** (`/document`): the header now describes the files the compiled program really uses and how (read, update…), the programs it calls and its service programs, read from the system; comments follow the source's style (free or fixed form), plus a short wiki summary.
- **Suggest unit tests** (`/test`): first the behaviours worth testing for each procedure (normal cases, boundaries, error paths, each branch), using the real procedure signatures and data structure layouts, then the RPGUnit test source and the RUCRTRPG / RUCALLTST commands.
- **Explain program dependencies** (`/depends LIB/PGM`, right-click a program or service program → *AI: Explain Program Dependencies*): modules and their sources, service programs, files used and how, programs and data areas referenced (DSPPGMREF), who is bound to a service program, and what to recompile, re-bind or promote together when something changes.
- **Recommend fixes from real job logs** (`/joblog number/user/name`, right-click a job, *Failed Jobs* → *Ask AI why it failed*, or the job log analysis page): reads the job log — or the spooled QPJOBLOG of an ended job —, finds the user program and statement where it failed, opens its source at that statement (SRCSEQ / *SRCSTMT mapping), and asks for the root cause and a concrete fix; a button opens the failing line.

**Faster and more reliable**

- **Pages open at once:** the 90 report pages (job details, object information, who is signed on, failed jobs, security, Work with…) open straight away with a loader — a spinner, what is being read, the seconds it takes and the outline of the page — instead of only a message in the status bar; refreshing a page shows a thin busy bar on it, as VS Code does. PDM, the System Tracker, the dashboard and the data editor use the same loader.
- **System Tracker opens at once:** the last page of the system is shown immediately while it refreshes, and the Overview is drawn as soon as its own figures are back; libraries, network, journals and the other tabs fill in when they arrive (*loading the rest…*).
- **PDM shows the member list first:** who has a member locked and whether its object is older than the source follow a moment later, without moving the cursor; options wait for them, so a locked member is still never deleted.
- **Report pages with thousands of rows** open at once: rows are drawn 300 at a time (*Show more*), the filter is instant, and every column sorts with a click.
- **Less waiting for the same list:** the library list, the objects of a library and the members of a source file are shared between the views for a short time instead of being read again by each one; Refresh (and any change you make) reads them again. Two views asking the same question at the same time now run it once.
- **The SQL engine starts as soon as you connect**, so the first view does not wait for Java on the IBM i; queries slower than 3 seconds and slow start-up steps are written to the Vanthrex log to find what is slow.
- **One look everywhere:** all pages share the same styles, loader, busy bar and paged / filtered / sortable table (`src/features/ui/kit.ts`), so they look and behave alike in light, dark and high-contrast themes.
- **Clearer code:** the modules that were named after release batches are now one module per subject (for example `dataStructures`, `programCall`, `jobTools`, `security`, `memberToolsView`, `sourceAnalysisView`), with their tests named the same way.

**New tools**

- **Source Quality Report** (right-click a source file): every RPG member checked — code checks, share of fixed format, numbered indicators, GOTO / CABxx, subroutines and procedures — with a score and a grade from A to E, lowest first, and the most frequent findings for the whole file.
- **Library list from a job description or a user profile**: see what changes, then replace your library list or add the missing libraries (*SYSVAL follows QUSRLIBL).
- **\*PUBLIC Authority Scan** (right-click a library, or *PUBLIC in the System Tracker): objects that give *ALL or *CHANGE to everybody, riskiest first, with a one-click fix to *PUBLIC *USE (asked first).
- **Copy to Another System…** (right-click a member or IFS file, or the editor menu, with two systems connected): copy a member or a stream file from one system to another — the target source file and member are created when missing, and you see how many lines change before anything is written; protected systems still ask.
- **Compare System Values with Another System** (Connections view with two systems connected, or the *All systems* tab): what differs between DEV and PROD, with the values that differ on purpose (dates, serial numbers, devices) kept apart.

## 2.2.0

**New: System Tracker — the whole system in one place**

- **One button** (the pulse icon in the Connections view, the inline button on the active connection, Ctrl+Alt+T, or the quick menu) opens a page with tabs:
  - **Overview:** system and release, CPU, system ASP use, jobs, waiting jobs, QSYSOPR replies, time since IPL, PTF level, libraries and your compile results as colour-coded tiles — and **Needs attention**: ASP almost full, inquiry messages, MSGW / LCKW jobs, high CPU, sources that did not compile, library list entries that do not exist, expired passwords — each with a button that takes you there.
  - **Libraries:** every library on the system with type, text, owner, created and last-used dates and its place in your library list; filter, sort, hide IBM libraries, and calculate objects and size on request. Each row: open in PDM, add to the library list, pin, storage advisor.
  - **Jobs:** waiting jobs (MSGW, LCKW), the top jobs by CPU and the subsystems — with details, job log and live job log on every job.
  - **Storage**, **QSYSOPR** (latest messages, inquiries highlighted, Explain, the sender's job log), **Users** (enabled, disabled, not signed on for 90 days, expired passwords, *ALLOBJ / *SECADM profiles), **PTFs & software** and **My work** (your jobs, spooled files, members changed in your library list in the last 7 days, broken compiles, pins).
- **Libraries tab shows every library** (it showed only QSYS: `OBJECT_STATISTICS('QSYS', '*LIB')` returns QSYS itself). Libraries are now read with `OBJECT_STATISTICS('*ALL', '*LIB')`, completed from the SQL catalog (SYSSCHEMAS). The same fix applies to PDM (WRKLIBPDM), Self-check and *Add library*, which could report existing libraries as missing.
- **Libraries tab:** tiles for libraries you can see, user and TEST libraries, your library list (and missing entries), libraries not used for a year (cleanup candidates), measured size and *your special authorities*; with *ALLOBJ every library is listed. Filter *Not used for a year*; *Calculate objects and size* now measures every library that passes the filters (not only the rows on screen), and sizes are remembered per system.
- **Storage tab:** largest libraries (measured). **Every table:** *Export CSV*. **Auto-refresh** every minute (header).
- **Jobs:** the counts are exact (the badge showed the 200-row query limit). The badge counts jobs waiting for a reply (MSGW); LCKW is counted only for batch and interactive jobs.
- **Health score:** the Overview opens with one number from 0 to 100 (✓ healthy, ⚠ keep an eye on it, ✗ action needed) and the reasons that lowered it (disk, messages waiting, MSGW jobs, CPU, QSECURITY, security settings…), with its trend.
- **Trends:** CPU, system ASP and jobs keep their history between refreshes (per system) and show a small trend line; CPU and ASP also show a meter. Problems are listed red first.
- **Queues tab:** job queues (held, or not attached to a subsystem, while jobs wait — flagged) and output queues by number of spooled files, with **Hold / Release** (asked first, protection respected).
- **Network tab:** every listening port with the service behind it (SSH, Telnet, host servers, Mapepire, DRDA…), its open connections, which services are not encrypted, and the addresses with the most connections.
- **Security settings** on the Users tab: QSECURITY, QPWDLVL, QMAXSIGN, QPWDEXPITV, QPWDMINLEN, QAUDCTL, QCRTAUT, QINACTITV and QALWOBJRST with ✓ / ⚠ / ✗ and what to change.
- **Copy summary:** a short Markdown summary of the system (score, key numbers, what needs attention) to paste into a chat or a ticket.
- **Scheduled jobs tab:** the whole job schedule (next run first, today's runs highlighted, held entries flagged) with **Hold / Release**.
- **Journals tab:** journals in user libraries, largest first — receivers kept, total size, journaled objects; 50+ receivers or 10 GB+ flagged for cleanup.
- **What changed tab:** objects changed today or in 7 days, or the largest objects — in your library list (fast) or every user library — with information, PDM and locks on each.
- **All systems tab:** every system you are connected to side by side (health score, CPU, ASP, MSGW, QSYSOPR replies) — *Open* switches to it.
- **Subsystems** with status and maximum jobs (full ones flagged), and **failed sign-on attempts** on the Users tab.
- **Save report:** the whole tracker as one HTML page (light theme, prints well) to send to your team or keep as a record.
- Every part is read independently: if one IBM i service is missing on a release or you are not authorized to it, the rest of the page still works and that part says why.

**Fixed**

- **Members could not be saved after PDM option 5** (issue #3): *Display* marked the member read-only for the whole VS Code session, so editing it later (option 2 or the Libraries view) showed a 🔒 and Ctrl+S did nothing. Option 5 now opens a separate read-only view; members already stuck are made editable again as soon as you switch to them.
- **A save no longer fails when the source-date save hits a technical problem** (QTEMP, SQL job…): the member is saved without source dates and you are told. Data problems (line too long, characters the CCSID cannot hold) still stop the save, so nothing is lost.
- **PDM option 14 compiled the active editor** instead of the member on the row; it now compiles each member you typed 14 on.

**New: history, live job logs and pins**

- **Compile History** (Libraries view menu, quick menu): every compile on this computer — when, which source, which object, ✓ / ✗ with errors and warnings, on which system. *Broken right now* lists the sources whose last compile failed, with **Recompile the broken sources** in one click.
- **Show My Changes Since the Last Compile** (editor menu, member menu, PDM option **SC**, or from *Objects Built from This Source*): highlights the lines changed after the program was last compiled, with a list to jump to each one.
- **Live Job Log** (right-click a job, or quick menu): new job log messages stream into an output panel every few seconds; escape messages and severity 30+ pop up with **Explain**; it stops by itself when the job ends.
- **Pinned view:** pin the members, source files, libraries, objects and IFS files you use every day (right-click → *Pin / Unpin*, or **PN** in PDM). One click opens a member, a source file or library in PDM, an object's information or an IFS file; pins are kept per system and can be reordered.
- **Batch compiles no longer stop on the first failure:** the error notification no longer has to be closed before the next member of a PDM option 14 batch, compile on save or *Recompile broken* runs.

**New: knowing what your source became**

- **Objects Built from This Source** (right-click a member or in the editor, or PDM option **OB**): every program and service program compiled from the member (QSYS2.PROGRAM_INFO for OPM, BOUND_MODULE_INFO for ILE modules), when, and whether the source changed after the compile — with *Compile now*.
- **Member status bar:** while you edit a member, the status bar shows ✓ the program it went into, ⚠ how many objects are out of date with your source, or that it was never compiled — and 🔒 who else has the member open. Click for details (`vanthrex.memberStatusBar`).
- **Compile on save** (`vanthrex.compileOnSave`: off / ask / always, optionally only for some source types): copy members are never compiled.
- **Find & Open Member…** (Ctrl+Alt+M) now searches your library list or every user library, accepts a source type (`ORD* RPGLE`), sorts by library-list order (first = what *LIBL would use) and opens the result in the editor, in PDM, or shows the objects built from it.

**New: PDM in one screen — Work with Libraries, Objects and Members using PDM**

- **The PDM you know, in VS Code:** right-click a library, a source file or a file and choose *Work with Using PDM…* (or the list button on the Libraries view, the quick menu, or type `WRKMBRPDM FILE(LIB/QRPGLESRC)`, `WRKOBJPDM LIB(X)`, `WRKLIBPDM LIB(A*)` or `STRPDM` in *Run CL Command*).
- **Type options and press Enter**, on as many rows as you like, with the PDM numbers: members 2 edit, 3 copy, 4 delete, 5 display (read-only), 6 print, 7 rename, 8 description, 13 change text and type, 14 compile, 15 create module, 16 local history, 25 find string, 54 compare two members; objects 4, 5, 7, 8, 11 move, 12 work with members, 13, 15 duplicate, 16 call, 18 edit data, 34 debug; libraries 5 / 12 work with objects, 8, 13. Deletes are confirmed once for the whole batch.
- **Function keys:** F3 exit, F5 refresh, F6 create (member, source file or library), F9 undo delete, F12 back, F13 repeat an option down the list, F16 user-defined options, F17 subset, F21 export the list to CSV, F23 more options. Shift+F1…F12 work as F13…F24 like in a 5250 emulator; ↑ / ↓ move between option fields.
- **All source files at once:** type `*ALL` (or a generic name like `Q*SRC`) in *File* — or `WRKMBRPDM FILE(MYLIB/*ALL)`, or option **AM** on a library — to list the members of every source file of a library in one list, with a *File* column; every option works across files.
- **Subset and position to:** generic names (ORD*, \*CUST\*), type, text, changed since, *Needs compile*, *In use*, or click a type chip (RPGLE 120, CLLE 30…); click a column to sort, double-click a row for its usual option.
- **User-defined options (F16)** with PDM variables &L &F &N &T &A &O &U &X, and parameters from the command line appended (for example `CB` + `TGTRLS(V7R4M0)`). Built-in: CB, CS, CC, DF, PF, RS (RUNSQLSTM) (`vanthrex.pdm.userOptions`).
- **Robust by design:**
  - **Undo delete (F9):** members removed with option 4 are copied first and can be put back with F9 (or `UNDO` on the command line); copies are also kept on disk. Members in use by another job are not deleted or renamed.
  - **Failed options stay on their rows** with the IBM i message (CPF…) in the Status column, so you fix and press Enter again — like PDM, but with the reason.
  - **Batches show progress and can be cancelled;** more than 10 changing options ask first. Renames to an existing name are stopped before they run.
- **See more at a glance:** an *Object* column (✓ up to date, ⚠ source changed after the last compile, ○ not compiled yet — in your object library), an *In use by* column with the job that has the member open, and a **preview pane** (tick *Preview*, click a member or move with the arrow keys).
- **Extras PDM never had:** Git history (GH), unused code (UC), hard-coded libraries (HL), where used (WU), who has it locked (LK), what depends on this file (DP), source files only (SF), add to library list (LL), set current library (CL), a status column per row and recently used lists.

## 2.1.0

**New: Security Admin center for users with *SECADM**

- **Shown only to security administrators.** Vanthrex checks whether you (or one of your group profiles) have *SECADM special authority; the *Security Admin* button and commands appear only then. Everyone else does not see them.
- **User profiles in one place:** every non-IBM profile with status, class, special authorities, group, last sign-on, failed sign-ons and password expiry; profiles with *ALLOBJ / *SECADM and locked-out profiles are highlighted.
- **Create a user** with a guided form (class, special authorities, group, current library, first password that must be changed at first sign-on — or no password for service accounts and groups), or **copy an existing user** (same class, authorities, groups, library, menu and job description).
- **Change, reset, enable / disable, expire the password, delete** a profile. Deleting asks what to do with the objects it owns (give them to another profile or delete them) and requires typing the profile name.
- **Unused profiles:** enabled profiles that have not signed on for 30–365 days, with **Disable all**.
- **Powerful profiles:** who has *ALLOBJ, *SECADM, *AUDIT, *SERVICE or a *SECOFR / *SECADM class, including the members of powerful groups.
- **Group profiles** with their members, and **authorization lists**: create one, add or remove users, change authorities, and see the objects it secures.
- **Passwords are never shown, stored or logged**: they are typed in hidden fields, and every command, confirmation, log line and error has them masked.

**Also new in 2.1**

- **Objects out of sync with their source** (right-click a library): programs, service programs, modules, commands and files whose source member changed after the last compile — or whose source member is gone — so you know what runs code that is not what the source shows.
- **What changed (release notes)** (right-click a library): source members and objects changed in the last 1–90 days, with **Copy as Markdown** for release notes or a code review.
- **New member from a template** (right-click a source file): RPG program, NOMAIN module, SQLRPGLE with a cursor, CL with error handling, binder source, SQL table, display file, physical file — or your own templates (`vanthrex.templates`).
- **Retrieve binder source** of a service program (RTVBNDSRC) and **work with binding directories** (add / remove entries).
- **Who is locking rows?** (right-click a file): every locked row with its job, status and the first columns of the row; open the job log or end the job.
- **Running SQL statements** (Jobs view toolbar): what SQL runs now and for how long, with **Cancel** (QSYS2.CANCEL_SQL).
- **Exit points and exit programs**: registered exit programs, and which network exit points (ODBC, FTP, remote command, file server…) have none.
- **Change owner or authority of many objects** (right-click a library): CHGOBJOWN for every matching object, or one GRTOBJAUT / RVKOBJAUT with a generic name.
- **Installed software and license keys**: every installed product option, and license keys with usage limits and expiry (expiring within 60 days highlighted).
- **Is this PTF installed?**: paste PTF IDs from an IBM page and see applied / loaded / superseded / not on the system.
- **Journals** (quick menu or right-click a library): every journal with its attached receiver, receiver count and size, objects journaled; change the receiver now (CHGJRN *GEN) or journal every new table of a library (STRJRNLIB).
- **IFS permissions** (right-click a file or folder): who has which data authority, the owner; change authority or owner, for a folder optionally everything below it.
- **Compare the structure of a table** between two libraries — or two connected systems: columns (type, length, nulls, default) and indexes, plus an ALTER TABLE script that makes the second copy match.
- **Find unused code** in an RPG source: standalone fields, constants, prototypes, subroutines and internal procedures nothing refers to.
- **Find hard-coded libraries** in a source or a whole source file: LIB/OBJECT names written into RPG, CL and SQL that break when code moves from DEV to PROD (`vanthrex.scan.allowedLibraries`).
- **Work with any message queue** (QSYSOPR by default): reply to waiting inquiry messages, remove messages, explain them, open the sender's job log, or send a message.
- **What is this job doing?** (right-click a job): status, current user, CPU, temporary storage, the SQL it runs, what it waits for, its call stack (your programs highlighted), the locks it holds and its activation groups.
- **System history log (QHST)**: messages of the last hours or days, filtered by severity, message ID or text, with Explain.
- **What depends on this file?** (right-click a file): logical files, indexes, views, constraints, triggers and foreign keys that use it.
- **Indicator usage** (right-click in an RPG or DDS editor): where each numbered indicator is set and tested, and the ones that are set but never tested (or the reverse).
- **IFS character set (CCSID)** (right-click a file or folder): the CCSID of each file, tag one file or a whole folder tree (CHGATR), or convert a file's text to UTF-8 or another CCSID.
- **Can the IBM i reach this host?**: PING from the IBM i itself, so firewall and DNS problems show up where the programs run.
- **Call a web API from the IBM i**: GET or POST through QSYS2.HTTP_*_VERBOSE, with headers, status and a formatted body — Authorization headers are never remembered.

## 2.0.0

**Vanthrex for IBM i 2.0 — 20 new features**

Development
- **Generate RPG code for a table** (right-click a file): a qualified data structure plus get / add / update / delete procedures and a cursor loop in embedded SQL, using the table's key.
- **Format SQL**: Db2 for i statements formatted with keywords in capitals and one clause per line (Shift+Alt+F in `.sql` files, or right-click → Format SQL).
- **Find and replace in a source file** (right-click a source file): text, whole word or regular expression across every member, with a preview of each line before anything changes; source dates are kept and changed lines get today's date; members someone has open are skipped.
- **Compile changed members** (right-click a source file): compile everything changed today, this week or this month — or pick members — with a result per member.
- **Print preview for printer files**: a PRTF drawn on a page, following SKIPB / SPACEB / SKIPA / SPACEA, with a field table that jumps to the source line.
- **Copy members to another source file** (CPYSRCF, keeps sequence numbers and dates) and **copy objects to another library** (CRTDUPOBJ, with or without data); **rename or move** an object.
- **Find a CL command** by a word from its name or description, then prompt it with F4.

Data
- **Export as SQL INSERT statements**, next to Excel, CSV and JSON.
- **Generate test data** for a table: rows that fit each column's type and length, keys continuing after the highest existing key, previewed before insert.
- **Find duplicate rows** by any columns.
- **Table statistics** of a library: rows, deleted rows, size, last change and last use.

Operations
- **Submit to batch and watch**: SBMJOB, then a status-bar spinner and a notification when the job ends — normally or not, with the job log and analysis one click away. **Watch This Job** does the same for any job in the Jobs view.
- **My recent jobs**: your jobs of the last days, abnormal ends highlighted.
- **Compare two spooled files** side by side — handy to check a program change did not alter a report.
- **Follow an IFS file** like `tail -f`, refreshed every 2 seconds.
- **Search text in IFS files** of a folder, optionally only some file names.
- **Library list sets**: save named library lists (DEV, TEST, a project…) per system and switch between them in one click.

All new screens are translated into the 7 languages.

## 1.3.0

**New: see your screens and your database, compare two systems, and share spooled files**

- **Screen preview for display files.** Open a DSPF member and click **Preview Screen** (editor title): the record format is drawn as it looks on a 5250 — constants, input fields (underlined), output fields, colors and display attributes, 24×80 or 27×132, windows, and a subfile control with its subfile rows. It follows the record your cursor is in and updates as you type; click a field to jump to its source line.
- **Database diagram.** Right-click a library → **Database Diagram**: the tables with their columns and primary keys, the foreign keys between them, and — because many IBM i databases never declared them — relationships inferred from column names (dashed). Click a table to highlight its links, zoom, **Copy as Mermaid** for Markdown / GitHub / wikis, or **Save as SVG**.
- **Compare with another system.** With two systems connected, compare a source member (VS Code diff), the objects of a library, the rows of a table by key, the system values, or the PTF group levels between DEV and PROD — the data is read from each system, so they never need to reach each other.
- **Spooled files to PDF and e-mail.** Right-click a spooled file → **Save as PDF…** or **Send by E-mail…**; in a `.sql` editor, **E-mail Query Result** sends the result as an Excel file. PDFs are made in VS Code from the spool text (or by the IBM i with `vanthrex.spool.pdfMode: server`); e-mail is sent by the IBM i with SNDSMTPEMM.
- All new screens are translated into the 7 languages.

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
