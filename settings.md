---
layout: default
title: "Settings"
nav_order: 2
parent: "Reference"
---

# Settings

Open **File → Preferences → Settings** and search for *Vanthrex*, or edit `settings.json`.

| Setting | Type | Default | Description |
|---|---|---|---|
| `vanthrex.compileActions` | array | 15 built-in actions | Compile actions. Variables: `&LIB` (source library), `&OBJLIB` (target library), `&SRCFILE`, `&NAME`, `&EXT`, `&FULLPATH` (IFS path), `&CURLIB`, `&USER`. Add `OPTION(*EVENTF)` to get inline errors. |
| `vanthrex.sql.maxRows` | number | `500` | Maximum number of rows fetched into the SQL result grid. |
| `vanthrex.sql.confirmDestructive` | boolean | `true` | Ask for confirmation before running DELETE, DROP, TRUNCATE or UPDATE without WHERE. |
| `vanthrex.tempDirectory` | string | `"/tmp"` | IFS directory used for temporary files during member transfer. |
| `vanthrex.spool.maxEntries` | number | `200` | Maximum number of spooled files listed. |
| `vanthrex.autoConnectLast` | boolean | `false` | Reconnect automatically to the last used system when VS Code starts. |
| `vanthrex.objects.showAll` | boolean | `true` | Show an 'Objects' folder (programs, files, service programs…) under each library. |
| `vanthrex.dashboard.refreshSeconds` | number | `30` | How often the System Dashboard refreshes (seconds). 0 = only when you click Refresh. |
| `vanthrex.dataEditor.pageSize` | number | `100` | Rows per page in the table data editor. |
| `vanthrex.history.enabled` | boolean | `true` | Keep a local copy of every member and IFS file you open or save, so you can compare and restore. |
| `vanthrex.history.maxVersions` | number | `50` | Local history versions kept per member / file. |
| `vanthrex.lint.enabled` | boolean | `true` | Check RPG sources as you type. |
| `vanthrex.lint.maxProcedureLines` | number | `200` | Report procedures longer than this many lines. |
| `vanthrex.lint.rules` | object | all checks on | Turn individual RPG checks on or off. |
| `vanthrex.sourceDates.enabled` | boolean | `true` | Read and save members **with** their sequence numbers and change dates (SRCSEQ/SRCDAT), like SEU. Unchanged lines keep their date; changed lines get today's date. Needs a Mapepire SQL engine; otherwise members are copied as plain text. |
| `vanthrex.sourceDates.display` | string | `"date"` | What to show in front of each member line (Ctrl+Alt+D cycles). Values: `date`, `seq-date`, `off`. |
| `vanthrex.sourceDates.format` | string | `"yymmdd"` | Date format: SEU-style YYMMDD or ISO YYYY-MM-DD. Values: `yymmdd`, `iso`. |
| `vanthrex.conflictCheck` | boolean | `true` | Warn when a member is locked by another job, or changed on the IBM i after you opened it, before your save overwrites it. |
| `vanthrex.members.sortBy` | string | `"name"` | Order of members in the Libraries view. Values: `name`, `date`. |
| `vanthrex.sql.scriptStopOnError` | boolean | `true` | Run SQL Script: stop at the first statement that fails (off = run every statement and report failures). |
| `vanthrex.debug.port` | number | `0` | IBM i Debug Service secured port. 0 = read it from the service configuration (usually 8005). |
| `vanthrex.debug.ignoreCertificateErrors` | boolean | `false` | Connect to the Debug Service even when its certificate cannot be verified. Only for test systems. |
| `vanthrex.debug.updateProductionFiles` | boolean | `false` | Allow the debugged program to update files in production libraries (UPDPROD). |
| `vanthrex.debug.trace` | boolean | `false` | Write a trace of the debug protocol to the IBM i Debug output (for support). |
| `vanthrex.connections.keepOthersOpen` | boolean | `true` | Keep other systems connected when you connect to another one, so you can switch between them instantly (Ctrl+Alt+S). |
| `vanthrex.callGraph.depth` | number | `2` | How many levels of callers / callees the call graph shows at first. |
| `vanthrex.callGraph.maxNodes` | number | `200` | Largest number of objects drawn in a call graph. |
| `vanthrex.callGraph.hideSystemObjects` | boolean | `true` | Leave IBM-supplied objects (QCMDEXC, QSYSPRT…) out of the call graph. |
| `vanthrex.ai.enabled` | boolean | `true` | Enable the @vanthrex AI assistant and the AI commands. Code you ask about is sent to the language model you selected in VS Code chat. |
| `vanthrex.ai.useTools` | boolean | `true` | Let the AI assistant look things up on the connected IBM i (object descriptions, table columns, source, read-only queries). |
| `vanthrex.ai.allowQueries` | boolean | `true` | Let the AI run read-only SQL queries (SELECT / WITH / VALUES only; anything that changes data is refused). |
| `vanthrex.ai.confirmQueries` | boolean | `true` | Ask before the AI runs a query on the IBM i. |
| `vanthrex.ai.maxSourceChars` | number | `60000` | Largest amount of source text sent to the language model in one request. |
| `vanthrex.alerts.enabled` | boolean | `false` | Show VS Code notifications when a job waits for a reply (MSGW), an inquiry arrives on QSYSOPR, a batch job ends abnormally or the system ASP passes the alert level. |
| `vanthrex.alerts.intervalSeconds` | number | `60` | How often live alerts check the IBM i, in seconds (30 or more). |
| `vanthrex.alerts.scope` | string | `"mine"` | Whose jobs and messages live alerts watch. Values: `mine`, `all`. |
| `vanthrex.alerts.diskPercent` | number | `85` | Alert when the system ASP is used above this percentage. |
| `vanthrex.promotion.backupLibrary` | string | `"QGPL"` | Library for the backup and transfer save files that object promotion creates. |
| `vanthrex.export.maxRows` | number | `100000` | Maximum number of rows exported to Excel, CSV or JSON. |
| `vanthrex.performance.intervalSeconds` | number | `5` | How often the performance monitor samples the IBM i, in seconds. |
| `vanthrex.rpgunit.library` | string | `"RPGUNIT"` | Library where RPGUnit (iRPGUnit) is installed; added to the library list to compile and run tests. |
| `vanthrex.rpgunit.testLibrary` | string | `""` | Library for the compiled test programs. Empty = your current library. |
| `vanthrex.selfCheck.onConnect` | boolean | `true` | Check the system the first time you connect to it in a session and warn about setup problems (SQL engine, CCSID, library list…). |
| `vanthrex.spool.pdfMode` | string | `"local"` | How spooled files become PDF: "local" converts the text in VS Code (works everywhere); "server" asks the IBM i (CPYSPLF WSCST(*PDF)) and keeps fonts and graphics, falling back to local. Values: `local`, `server`. |
| `vanthrex.compare.maxRows` | number | `50000` | Maximum rows read from each system when comparing a table across two systems. |
| `vanthrex.ifs.followLines` | number | `500` | How many lines at the end of a file "Follow File (tail -f)" shows; it refreshes every 2 seconds. |
| `vanthrex.templates` | array | `[]` | Your own templates for "New Member from Template…": name, source type (RPGLE, CLLE, SQL…), description and text. &NAME, &TEXT, &DATE and &USER are filled in. |
| `vanthrex.scan.allowedLibraries` | array | `[]` | Libraries that may be named in source without being reported by "Find Hard-Coded Libraries" (IBM libraries and QTEMP are always allowed). |
| `vanthrex.pdm.userOptions` | object | `{}` | PDM user-defined options (F16): option code → CL command. Variables: `&L` library, `&F` file, `&N` name, `&T` type, `&A` attribute, `&O` object library, `&U` user, `&X` text. Built-in: CB, CS, CC, DF, PF, RS (set one to an empty string to hide it). |
| `vanthrex.compileOnSave` | string | `"off"` | Compile a source member after you save it: `off`, `ask` (a notification with Compile / Always / Not now) or `always`. Copy members (INC, RPGLEINC…) are never compiled. Values: `off`, `ask`, `always`. |
| `vanthrex.compileOnSave.types` | array | `[]` | Only compile on save these source types (for example `RPGLE`, `SQLRPGLE`). Empty = every type that can be compiled. |
| `vanthrex.memberStatusBar` | boolean | `true` | Show, for the member you are editing, whether its program is up to date with the source and who else has it open (status bar; click for details). |
| `vanthrex.connections.autoReconnect` | boolean | `true` | When a connection drops (network, VPN, sleep), reconnect by itself with the saved sign-on: 5 attempts over about 2 minutes. Changes that could not be saved meanwhile are kept on this computer and saved when the system is back. |
| `vanthrex.connections.healthCheckSeconds` | number | `60` | Check every N seconds that the active system still answers (a tiny query). A slow answer shows in the status bar; two misses in a row reconnect. `0` turns it off. |
| `vanthrex.notes.sharedFile` | string | `""` | Share member notes with your team: an IFS file such as `/home/TEAM/vanthrex-notes.json` that everybody can read and write. Empty keeps notes on this computer only. |
| `vanthrex.dsLayout.hover` | boolean | `true` | Show the position and length of a data structure subfield when you hover over its definition. |
| `vanthrex.5250.client` | string | `"auto"` | Which program opens a 5250 session for the active system. Values: `auto`, `acs`, `tn5250`, `command`. |
| `vanthrex.5250.acsPath` | string | `""` | Path to acslaunch_win-64.exe, acslaunch_linux-64, the ACS app or acsbundle.jar (empty: found automatically). |
| `vanthrex.5250.command` | string | `""` | Command that starts your 5250 emulator, with `${host}`, `${user}`, `${device}` and `${port}` replaced, for example `"C:\\Program Files\\IBM\\Client Access\\Emulator\\pcsws.exe" /H=${host}`. |
| `vanthrex.5250.deviceName` | string | `""` | Display device name to use (tn5250 and your own command). |
| `vanthrex.5250.ssl` | boolean | `false` | Use TLS (port 992) for tn5250. |
| `vanthrex.5250.port` | number | `0` | Telnet port when it is not the default (23, or 992 with TLS). |
| `vanthrex.deploy.directory` | string | `""` | IFS folder a local workspace folder is deployed to. `${home}`, `${user}` and `${folder}` are replaced. Empty: `${home}/builds/${folder}`. |
| `vanthrex.deploy.ignore` | array | `["node_modules/", ".vscode/", "*.vsix", "*.log", ".env", ".env.*", "*.pem", "*.key"]` | Files and folders that are never deployed (`*` and `**` wildcards, a trailing `/` for folders). `.git` is always skipped. |
| `vanthrex.deploy.buildCommand` | string | `""` | Command **Build Project on IBM i** runs in PASE in the deploy folder, for example `makei build` (Bob) or `gmake`. `CURLIB` and `LIBL` are set from the connection. |
| `vanthrex.deploy.ccsid` | number | `1208` | CCSID the deployed files are tagged with (1208 = UTF-8, so compilers read them correctly). 0 leaves the tag alone. |
| `vanthrex.deploy.onSave` | boolean | `false` | Upload a local file to its deploy folder every time it is saved. |
| `vanthrex.deploy.compileDeploysChanges` | boolean | `true` | Before compiling a local file, deploy every changed file of the folder too (so changed copybooks and includes are used). |
| `vanthrex.terminal.openSourcePath` | boolean | `true` | Put `/QOpenSys/pkgs/bin` (yum open-source tools: bash, git, python…) first on the PATH of a new PASE terminal. |
| `vanthrex.notebook.maxRows` | number | `1000` | Rows an SQL cell of an IBM i notebook reads (a cell can ask for more with `-- rows: N`). |
| `vanthrex.editor.columnHints` | boolean | `true` | Show the fixed-format field under the cursor (RPG and DDS) in the status bar. |
| `vanthrex.editor.rpgIndent` | number | `2` | Spaces per level when **Format Document** re-indents fully free RPG. |
| `vanthrex.editor.clCommandHelp` | boolean | `true` | In CL sources, show what a command does when you hover it and offer its keywords and allowed values while typing (read from the command definitions on the connected system). |
| `vanthrex.editor.sqlCodeLens` | boolean | `true` | Show **Run**, **Explain** and **RPG code** links above each statement of an SQL file. |
| `vanthrex.codeGen.arraySize` | number | `100` | Number of elements (`dim`) of arrays in generated RPG (JSON arrays, rows read per FETCH). |
| `vanthrex.codeGen.insertRows` | number | `1000` | Rows **Copy Rows as SQL INSERT Script** reads at most. |
| `vanthrex.ai.redact.secrets` | boolean | `true` | Before anything is sent to the AI, replace passwords (CL `PASSWORD(…)`, `pwd = …`), API keys, tokens, private keys and credentials in URLs by placeholders (xxxx1, xxxx2…). The real values are put back only on this computer, in the answer. |
| `vanthrex.ai.redact.personalData` | boolean | `true` | Replace e-mail addresses, payment card numbers (Luhn-checked) and IBANs (checksum-checked) by placeholders before they are sent to the AI. |
| `vanthrex.ai.redact.hostNames` | boolean | `true` | Replace IP addresses and the host names of your connections (and of `vanthrex.ai.redact.hostList`) by placeholders before they are sent to the AI. |
| `vanthrex.ai.redact.hostList` | array | `[]` | More internal host or server names to hide from the AI. |
| `vanthrex.ai.redact.words` | array | `[]` | Words that must never be sent to the AI (customer names, project code names…): replaced by placeholders. |
| `vanthrex.ai.sensitiveColumns` | array | `["PASS", "PWD", "SECRET", "TOKEN", "APIKEY", "SSN", "SOCSEC", "NIR", "IBAN", "BIC", "SWIFT", "CARD", "CCNUM", "CVV", "PAN", "SALARY", "SALAIRE", "WAGE", "PAYRATE", "BIRTH", "DOB", "TAXID", "NATID", "PASSPORT", "EMAIL", "MAIL", "PHONE", "TEL", "MOBILE", "ADDRESS", "ADR"]` | Columns whose values are always replaced by `xxxx` in query results sent to the AI (a column matches when its name contains the word; short words must be a whole part of the name). |
| `vanthrex.ai.deniedLibraries` | array | `[]` | Libraries the AI may never read (source, objects, queries, authorities). `PAY*` matches every library starting with PAY. |
| `vanthrex.ai.productionData` | string | `"metadata"` | What the AI may read on **protected** connections (production protection *Confirm* or *Read-only*): `metadata` = source, catalog and object facts but no table rows (default), `full` = also query results (masked), `none` = nothing. Values: `full`, `metadata`, `none`. |
| `vanthrex.ai.otherSystemsData` | string | `"full"` | What the AI may read on connections that are not protected: `full` (query results are still masked), `metadata` or `none`. Values: `full`, `metadata`, `none`. |
| `vanthrex.ai.audit` | boolean | `true` | Keep an audit trail of what is sent to the AI (time, system, feature, size, number of hidden values — never the content) in the *Vanthrex AI Audit* output and a file in the extension's storage. |
| `vanthrex.ai.showPrivacyNote` | boolean | `true` | After an answer, say how many values were hidden from the AI. |
| `vanthrex.ai.codeLens` | boolean | `true` | Show ✨ **Explain · Document · Tests** above each RPG procedure and subroutine. |
| `vanthrex.ai.modelFamily` | string | `""` | Language model family for **AI: Change the Selected Code** (for example `gpt-4o` or `claude-sonnet-4`); empty = the first available model. The chat uses the model chosen in the chat window. |
| `vanthrex.editor.checkCharacters` | boolean | `true` | Underline characters that break a compile or a CCSID conversion (tabs, control characters, no-break spaces, curly quotes, characters lost in a conversion) when a source is opened or saved. |
| `vanthrex.csvSeparator` | string | `","` | Separator of CSV files written by **Report to CSV** (`;` for spreadsheets set up for a comma as decimal separator). Values: `,`, `;`, `	`. |
| `vanthrex.jobHistoryDays` | number | `30` | Days of history log read by **Job Run History**. |

## RPG check rules

Use `vanthrex.lint.rules` to switch single checks off, for example:

```json
"vanthrex.lint.rules": { "numbered-indicator": false, "select-star": false }
```

| Rule | What it reports |
|---|---|
| `unused-definition` | Variables, constants and subroutines that are declared but never used |
| `goto` | GOTO usage |
| `tag` | TAG labels |
| `program-end` | Main program without *INLR = *ON or RETURN |
| `long-procedure` | Procedures longer than the configured number of lines |
| `numbered-indicator` | Numbered indicators (*IN01-*IN99) |
| `empty-on-error` | ON-ERROR blocks that silently swallow errors |
| `select-star` | SELECT * in embedded SQL |
| `mixed-format` | Fixed-format calculation specs in a free-format source |

## Compile actions

These are the built-in entries of `vanthrex.compileActions`. Copy one into your settings to change it, or add your own.

Variables: `&LIB` (source library), `&OBJLIB` (object library), `&SRCFILE`, `&NAME`, `&EXT`, `&FULLPATH` (IFS path), `&CURLIB`, `&USER`.

| Name | Source types | From | Command |
|---|---|---|---|
| Create Bound RPG Program (CRTBNDRPG) | rpgle | member | `CRTBNDRPG PGM(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)` |
| Create RPG Module (CRTRPGMOD) | rpgle | member | `CRTRPGMOD MODULE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)` |
| Create SQL RPG Program (CRTSQLRPGI) | sqlrpgle | member | `CRTSQLRPGI OBJ(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OBJTYPE(*PGM) COMMIT(*NONE) OPTION(*EVENTF) DBGVIEW(*SOURCE) CLOSQLCSR(*ENDMOD) REPLACE(*YES)` |
| Create Bound CL Program (CRTBNDCL) | clle | member | `CRTBNDCL PGM(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)` |
| Create CL Program (CRTCLPGM) | clp | member | `CRTCLPGM PGM(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) REPLACE(*YES)` |
| Create Command (CRTCMD) | cmd | member | `CRTCMD CMD(&OBJLIB/&NAME) PGM(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) REPLACE(*YES)` |
| Create Physical File (CRTPF) | pf | member | `CRTPF FILE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF)` |
| Create Logical File (CRTLF) | lf | member | `CRTLF FILE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF)` |
| Create Display File (CRTDSPF) | dspf | member | `CRTDSPF FILE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) REPLACE(*YES)` |
| Create Printer File (CRTPRTF) | prtf | member | `CRTPRTF FILE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) REPLACE(*YES)` |
| Run SQL Script (RUNSQLSTM) | sql | member | `RUNSQLSTM SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) COMMIT(*NONE) NAMING(*SQL)` |
| Create Bound RPG Program from IFS (CRTBNDRPG) | rpgle | ifs | `CRTBNDRPG PGM(&OBJLIB/&NAME) SRCSTMF('&FULLPATH') OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES) TGTCCSID(*JOB)` |
| Create SQL RPG Program from IFS (CRTSQLRPGI) | sqlrpgle | ifs | `CRTSQLRPGI OBJ(&OBJLIB/&NAME) SRCSTMF('&FULLPATH') OBJTYPE(*PGM) COMMIT(*NONE) OPTION(*EVENTF) DBGVIEW(*SOURCE) CVTCCSID(*JOB) REPLACE(*YES)` |
| Create Bound CL Program from IFS (CRTBNDCL) | clle | ifs | `CRTBNDCL PGM(&OBJLIB/&NAME) SRCSTMF('&FULLPATH') OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)` |
| Run SQL Script from IFS (RUNSQLSTM) | sql | ifs | `RUNSQLSTM SRCSTMF('&FULLPATH') COMMIT(*NONE) NAMING(*SQL)` |

```json
"vanthrex.compileActions": [
  {
    "name": "Create RPG program into my test library",
    "extensions": ["rpgle"],
    "source": "member",
    "command": "CRTBNDRPG PGM(MYTEST/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)"
  }
]
```

Keep `OPTION(*EVENTF)` so the errors can be shown inline.
