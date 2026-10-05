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
| `vanthrex.git.authorName` | string | empty | Name used for commits made by Vanthrex's Git commands (empty = your Git configuration). |
| `vanthrex.git.authorEmail` | string | empty | E-mail used for commits made by Vanthrex's Git commands (empty = your Git configuration). |
| `vanthrex.ai.enabled` | boolean | `true` | Enable the @vanthrex AI assistant and the AI commands. Code you ask about is sent to the language model you selected in VS Code chat. |
| `vanthrex.ai.useTools` | boolean | `true` | Let the AI assistant look things up on the connected IBM i (object descriptions, table columns, source, read-only queries). |
| `vanthrex.ai.allowQueries` | boolean | `true` | Let the AI run read-only SQL queries (SELECT / WITH / VALUES only; anything that changes data is refused). |
| `vanthrex.ai.confirmQueries` | boolean | `true` | Ask before the AI runs a query on the IBM i. |
| `vanthrex.ai.maxSourceChars` | number | `60000` | Largest amount of source text sent to the language model in one request. |

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
