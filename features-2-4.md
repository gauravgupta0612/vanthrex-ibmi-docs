---
layout: default
title: "New in 2.4"
nav_order: 27
parent: "Features"
---

# New in 2.4: local development, notebooks and a smarter editor
{: .no_toc }

Work from a local Git folder and build on the IBM i, open a PASE shell, keep SQL / CL / shell runbooks as notebooks with charts, find who gets which SQL error, browse a schema, call stored procedures, generate RPG from queries and JSON, get CL command help and quick fixes, and do more with the IFS and job descriptions.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Local development

| Step | How | What happens |
|---|---|---|
| Deploy | Explorer right-click → *Deploy Changes to IBM i (IFS)* | New and changed files go to `${home}/builds/<folder>` (or `vanthrex.deploy.directory`), folders created, files tagged CCSID 1208. `.git`, `node_modules`, `.vscode`, keys, `.env` and logs are never sent. |
| Compile | Ctrl+Alt+C or ▶ in the editor title on a local file | Changed files are deployed, the stream file is compiled with your IFS compile actions, errors show on the **local** file (and local copybook). |
| Build | *Build Project on IBM i* | Your command (`makei build`, `gmake`, a script) runs in PASE in the deploy folder with `/QOpenSys/pkgs/bin` on the PATH and `CURLIB` / `LIBL` set; output in the *Vanthrex Build* panel. |
| Shell | **Ctrl+Alt+P**, terminal **+** → *IBM i (PASE)*, IFS folder → *Open PASE Terminal Here* | An interactive shell over the connection you already have. |

Settings: `vanthrex.deploy.directory`, `vanthrex.deploy.ignore`, `vanthrex.deploy.buildCommand`, `vanthrex.deploy.ccsid`, `vanthrex.deploy.onSave`, `vanthrex.deploy.compileDeploysChanges`, `vanthrex.terminal.openSourcePath`.

## IBM i notebooks and charts

*New IBM i Notebook* creates a `.vxnb` file with SQL, CL and PASE shell cells and Markdown text. Run a cell with **Shift+Enter**.

| Cell | Shows |
|---|---|
| SQL | A result table (not saved in the file). `-- chart: bar|line|pie Title` on the first line draws a chart; `-- rows: 5000` reads more rows. |
| CL | Every message, and the printed output of display commands (DSPLIBL, DSPJOB…). |
| Shell | The command's output. |

*Export Notebook to Markdown* (notebook toolbar) writes the cells and their last results for a ticket or a wiki.

## SQL Error Log

*SQL Error Log (Who Gets Which SQL Error?)* reads the SQL Error Logging Facility (SELF, IBM i 7.4 TR7 / 7.5 TR1 and later): which programs and jobs got which SQLCODE, how often, with which statement — most frequent first, each one explained in a click. *Turn SQL Error Logging On or Off…* sets it for the whole system (`*ERR`, `*ALL`, codes such as `-204, -803`, `*NONE`; needs *SECADM) or only for your session.

## Schema browser and stored procedures

Right-click a library → *Browse Schema (SQL Objects)…*: tables, views, indexes, aliases, procedures, functions, triggers, sequences and global variables with long and system names. Click one for its CREATE statement, its data, what depends on it, or to call it.

*Call Stored Procedure…* asks for each parameter with its SQL type (checked as you type; `NULL`; empty = default), and shows the OUT / INOUT values and the result set. OUT values come back through global variables in QTEMP (Mapepire SQL engine).

## Editor

| Feature | RPG | CL |
|---|---|---|
| Folding | Procedures, DS / PR / PI, IF, DO, FOR, SELECT, MONITOR, BEGSR, P-specs (free and fixed) | DO / ENDDO (also `THEN(DO)`), SELECT, SUBR |
| Parameter hints | Prototypes and procedure interfaces in the source, common built-in functions | — |
| Format Document | Fully free (`**FREE`) sources, `vanthrex.editor.rpgIndent` | — |
| Outline / definition / references | (already there) | Variables, files, labels, subroutines; `&var`, `GOTO`, `CALLSUBR` |
| Fixed-format fields | Status bar shows the field under the cursor; **Ctrl+Alt+]** / **Ctrl+Alt+[** jump between fields (also DDS) | — |

## IFS folders

Right-click an IFS folder → *Upload Files or a Folder Here…*, or drag files and folders from the Explorer or the desktop onto the IFS view. Right-click a file or folder → *Download to This PC…*. Whole trees in one step; `.git` is skipped; one question before replacing.

## CL help, quick fixes and command sources

| Feature | How |
|---|---|
| CL command help | Hover a command in a CL source: what it does and every parameter. While typing, the keywords not used yet (with their default) and, inside `KWD(`, the allowed values. Read from the connected system, so your own commands work too (`vanthrex.editor.clCommandHelp`). |
| Quick fixes | After a compile, **Ctrl+.** on *RNF7030 name not defined* → *Declare it here* or *Declare it globally*; unused declarations (*RNF7031*) are faded with *Remove unused declaration*. |
| Command sources (.cmd) | What CRTCMD would reject is underlined as you type; *Preview Command Prompt (F4) from Source* shows the prompt and builds the command from the values you try. |
| Retrieve CL Source | Right-click a CL program → *Retrieve CL Source (RTVCLSRC)*. |

## SQL and code generation

- **Run / Explain / RPG code** links above every statement of a `.sql` file (`vanthrex.editor.sqlCodeLens`).
- **Generate RPG for This Query**: column types read from the system, a cursor and a multi-row FETCH loop, null indicators when needed.
- **Generate RPG from a JSON Sample**: templates, `dim()` arrays with count fields, RPG-valid names, and the DATA-INTO / DATA-GEN statements.
- **Find a Value in Table Data…**: the rows (and the column) where a value is, in any column of a file.
- **Copy Rows as SQL INSERT Script…**: rows chosen with a WHERE condition as `INSERT … WITH NC` statements.
- **My SQL Job**: library list and job log of the job that runs Vanthrex's SQL.

## More for the IFS and work management

- **Compare Folder with IFS…**: newer / different / only-on-one-side files, with diff, upload or download per file.
- **Extract Here…** and **Compress (zip / tar)…** on IFS files and folders.
- **Copy To…** and **Move or Rename…** for IFS files and folders.
- **Work with Job Descriptions**: user, job queue, initial library list, logging; change the library list or job queue, or use the library list for your connection.
