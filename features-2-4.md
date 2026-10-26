---
layout: default
title: "New in 2.4"
nav_order: 27
parent: "Features"
---

# New in 2.4: local development, notebooks and a smarter editor
{: .no_toc }

Work from a local Git folder and build on the IBM i, open a PASE shell, keep SQL / CL / shell runbooks as notebooks with charts, find who gets which SQL error, browse a schema, call stored procedures, and get folding, parameter hints, formatting and CL navigation in the editor.
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
