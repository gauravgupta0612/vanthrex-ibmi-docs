---
layout: default
title: "New in 2.6"
parent: "What's new"
nav_order: 5
---

# New in 2.6
{: .no_toc }

Daily RPG development: about 150 small features that work on the open source, instantly and offline.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## 19 new code checks

![Quick fix after CHAIN]({{ "/images/quick-fix.png" | relative_url }})
*Ctrl+. on a warning adds the missing code — here an IF NOT %FOUND test after CHAIN.*

Each one can be switched off in `vanthrex.lint.rules`.

- Old fixed-format operation codes (MOVE, Z-ADD, CAT, SCAN…) with their free-form equivalent, and a quick fix that converts the line.
- CHAIN not followed by `%FOUND`, embedded SQL whose SQLCODE / SQLSTATE is never tested, cursors opened but never closed.
- `DSPLY` left in the code, statements after RETURN / LEAVE / ITER that never run, empty IF / DOW / FOR / MONITOR blocks, SELECT without OTHER.
- A literal longer than the field it is assigned to, a name declared twice, blocks nested deeper than `vanthrex.lint.maxNesting` (6).
- Procedures: input parameters that could be CONST, unused parameters, a return value with no RETURN, procedures neither exported nor called, more than 8 parameters.
- Free-form programs without CTL-OPT, code after column 80 in column-limited sources, large blocks of commented-out code.
- Quick fixes for most of them: add CONST, remove the DSPLY or unreachable line, insert CTL-OPT, an `IF NOT %FOUND`, an SQLCODE test or OTHER, wrap the long line.

## Editing


- **Close the Open Block** (Ctrl+Alt+.) and automatic `ENDIF` / `ENDDO` / `ENDFOR` / `ENDSL` / `ENDMON` / `ENDSR` / `END-PROC` on Enter (`vanthrex.editor.autoCloseBlocks`).
- **Surround With…** (Ctrl+Alt+W): IF, MONITOR, DOW, FOR, SELECT, BEGSR or a comment around the selection.
- **Convert IF / ELSEIF to SELECT / WHEN**.
- **Toggle RPG Comment** (Ctrl+/): `//` in free form, `*` in column 7 in fixed form.
- **Change Keyword Case…**: operation codes and keywords to lower or upper case, names and literals untouched.
- **Sort Declarations by Name** and **Align Declarations** for a block of DCL-S / DCL-C.
- **Wrap Long Line** at `vanthrex.editor.wrapColumn` (80 in column-limited sources), **Insert Column Ruler**, **Clear Change Markers** (columns 1-5).
- **Format Embedded SQL** under the cursor, in place.
- **Insert Procedure Skeleton…** and a documentation header from the procedure interface.
- **Add DCL-PR From the Source Index**: the prototype of a procedure of another member, built from its DCL-PI.
- Expand selection by statement and block (Shift+Alt+→) in RPG and CL.
- 10 new snippets: PSDS, INFDS, NOMAIN module, procedure with MONITOR, SQL INSERT / UPDATE with SQLCODE test, SQL cursor loop, QCMDEXC, DATA-INTO JSON, date arithmetic.

## Navigation and help


- **Go to Next / Previous Procedure** (Ctrl+Alt+PageDown / PageUp) and the current procedure in the status bar.
- Parameter names shown before call arguments (inlay hints), reference counts above procedures (`vanthrex.editor.referenceCodeLens`, off by default).
- **Call hierarchy** (Shift+Alt+H) for procedures and subroutines; procedures of all indexed sources in **Go to Symbol in Workspace** (Ctrl+T).
- Completion of the names declared in the source, procedure calls with their parameters, and subroutines after EXSR.
- Hover on `/COPY` and `/INCLUDE` shows the start of the member.
- Fixed-format RPG: the column fields of the current line are shaded with their name on hover.
- **Open IBM Documentation for the Word** under the cursor (release in `vanthrex.editor.docsRelease`).

## Suggestions while you type

![Suggestion while typing]({{ "/images/suggestions.png" | relative_url }})
*The next line appears in grey; Tab accepts it.*

Shown in grey: **Tab** accepts, Esc ignores.

- **The next statement you usually write**, offline and instant: `IF %FOUND(file)` after CHAIN, `READE` / `READ` after SETLL, `EXEC SQL OPEN` after DECLARE CURSOR and `FETCH NEXT` after OPEN, an SQLCODE test after SELECT INTO / INSERT / UPDATE / DELETE / FETCH, `DCL-PI` after `DCL-PROC`, CTL-OPT right after `**FREE`.
- **The type of a new variable** from its name and from the variables already declared (`dcl-s custName` → the type of `shipName`; `…Date` → `date`, `…Total` → `packed(11:2)`, `is…` → `ind`, `…Count` → `int(10)`, `…Stmt` → `varchar(3000)`).
- **The file of `%FOUND(` / `%EOF(` / `%EQUAL(`** from the last CHAIN, SETLL or READ, **the parameters of a call** (`calc(` → `custNo: amount);`), `*INLR = *ON;`, the usual CTL-OPT, DCL-F and DCL-DS keywords.
- **CL**: the MONMSG that usually follows a command, with its message (CHKOBJ → CPF9801, DLTF → CPF2105, CRTLIB → CPF2111, ADDLIBLE → CPF2103… 29 commands), DCL for the PGM PARM parameters not declared yet, and a TYPE / LEN from the variable name.
- Nothing is suggested inside a comment or a literal, in the middle of a line, or in fixed-format specs. **Turn IBM i Suggestions On or Off** (`vanthrex.editor.inlineSuggestions`).
- **AI suggestions (off by default)**: `vanthrex.ai.inlineSuggestions` also asks your AI model when you pause typing (`vanthrex.ai.inlineDelay`, 500 ms) and no offline suggestion applies, in RPG, CL, SQL and DDS. The code around the cursor goes through the same guard as the chat (secrets and personal data replaced, denied libraries and protected systems never sent, every request in the audit trail); after three failures in a row it stops until turned on again. **AI: Turn Suggestions While Typing On or Off** asks for confirmation first.

## Developer Toolbox

![Developer Toolbox]({{ "/images/developer-toolbox.png" | relative_url }})
*Ctrl+Alt+A: every tool that fits the file you are in.*

Every tool in one menu: **Ctrl+Alt+A**, the **IBM i** button in the status bar, or right-click → *IBM i Tools for This Source*.

- The menu shows only what fits where you are: the language of the file (RPG, CL, SQL, DDS) and whether text is selected, grouped (Rewrite, Generate, SQL, Edit, Copy, Select, Fix all, Help), searchable. The 2.6 commands are in it too, so nothing has to be remembered.
- **Rewrite RPG**: compound assignments (`x = x + 1` → `x += 1`, only when the meaning stays the same), EVAL / CALLP removed, a condition negated (`=` ↔ `<>`, NOT added or removed), `= *ON` / `= *OFF` simplified, a value wrapped with a built-in (%TRIM, %CHAR, %DEC, %UPPER, %SCANRPL… 23 of them), DCL-S lines grouped in a qualified DS, a subroutine converted to a procedure (EXSR x → x(), LEAVESR → RETURN), `NAME value` lines to DCL-C.
- **Generate**: SQL INSERT / SELECT INTO / UPDATE from a data structure, a DS template from CREATE TABLE and CREATE TABLE from a DS, a program header (author, date, change history), a section separator, date / time / timestamp literals, a global CL error handler (MONMSG CPF0000 → ERROR: that resends the message).
- **SQL**: how many rows will change (`SELECT COUNT(*)` added above an UPDATE / DELETE), limit a SELECT to 100 rows, SQL to embedded SQL (`?` → `:host`) and embedded SQL to a runnable script, SQL keywords upper / lower, lines to an `IN (…)` list, CSV lines to VALUES / INSERT, and **WHERE** suggested while typing after UPDATE … SET or DELETE FROM.
- **Fix all at once**: declare every undeclared SQL host variable, add CONST to every read-only parameter, remove every DSPLY (after a confirmation), declare every undeclared CL variable.
- **Edit and copy**: keep a line as a comment (with your name and the date) before changing it, a literal from the selection, aligned `=` signs and end-of-line comments, blank lines removed, the source cleaned (tabs, trailing blanks, invisible spaces), CL in upper case and long CL commands wrapped with `+`; copy as Markdown, a reference to the line (`LIB/FILE(MBR) line 42`), the compile command of the member (CRTBNDRPG, CRTSQLRPGI, CRTBNDCL, CRTPF, CRTDSPF… 14 types), a CL command as `CALL QSYS2.QCMDEXC(…)`, the DCL-PR or a call of the procedure.
- **Select** the current block or procedure; **What is new in 2.6** opens this page.
- **Hovers**: a literal shows its length (bytes for `X'…'`), a declared RPG variable its storage size (`vanthrex.editor.sizeHovers`).

### All the tools

| Tool | Group | For |
|---|---|---|
| Use compound assignments (x += 1) | Rewrite | RPGLE |
| Remove EVAL and CALLP | Rewrite | RPGLE |
| Negate the condition | Rewrite | RPGLE |
| Simplify "= *ON" / "= *OFF" | Rewrite | RPGLE |
| Wrap with a built-in function… | Rewrite | RPGLE |
| Group the variables in a data structure | Rewrite | RPGLE (selection) |
| Convert a subroutine to a procedure | Rewrite | RPGLE |
| Lines to named constants | Rewrite | RPGLE (selection) |
| SQL INSERT / SELECT / UPDATE from this data structure | Generate | RPGLE |
| Data structure from CREATE TABLE | Generate | all sources (selection) |
| CREATE TABLE from this data structure | Generate | RPGLE |
| Insert a program header | Generate | RPGLE |
| Insert a section separator | Generate | RPGLE |
| Insert a date / time literal | Generate | RPGLE, SQL, CL |
| Keep the line as a comment before changing it | Edit | RPGLE, CL |
| Copy the prototype of this procedure | Copy | RPGLE |
| Copy a call of this procedure | Copy | RPGLE |
| Open this embedded SQL as a script | SQL | RPGLE |
| Declare all undeclared SQL host variables | Fix all | RPGLE |
| Add CONST to every read-only parameter | Fix all | RPGLE |
| Remove all DSPLY | Fix all | RPGLE |
| Select the current block | Select | RPGLE, CL |
| Select the current procedure | Select | RPGLE |
| Declare all undeclared CL variables | Fix all | CL |
| Add a global error handler | Generate | CL |
| CL in upper case | Rewrite | CL |
| Wrap the long CL command (+) | Rewrite | CL |
| Copy as an SQL call (QSYS2.QCMDEXC) | Copy | CL |
| How many rows will change? (COUNT first) | SQL | SQL |
| Limit to 100 rows | SQL | SQL |
| Copy as embedded SQL for RPG | SQL | SQL |
| SQL keywords in upper / lower case | SQL | SQL, RPGLE |
| Lines to an SQL IN list | SQL | all sources (selection) |
| CSV lines to SQL VALUES / INSERT | SQL | all sources (selection) |
| Selection to a literal | Edit | all sources (selection) |
| Align the = signs | Edit | RPGLE, all sources (selection) |
| Align end-of-line comments | Edit | RPGLE, all sources (selection) |
| Remove blank lines | Edit | all sources (selection) |
| Clean up the source | Edit | all sources |
| Copy as Markdown | Copy | all sources |
| Copy a reference to this line | Copy | all sources |
| Copy the compile command | Copy | RPGLE, CL, SQL, DDS |
| What is new in 2.6 | Help | all sources |

## CL checks while you type

![CL checks]({{ "/images/cl-checks.png" | relative_url }})
*CL checks in the Problems view.*

Switched with `vanthrex.lint.cl`, and each one in `vanthrex.lint.rules`.

- Variables used but not declared (quick fix: a DCL with a type from the name) and declared but never used (quick fix: remove the DCL).
- GOTO to a label that does not exist; DO / DOWHILE / DOUNTIL / DOFOR / SELECT / SUBR not closed, or an ENDDO too many.
- DCL / DCLF after the first command; a literal longer than the `*CHAR` variable (it is cut); text that is not a number put in a `*DEC` / `*INT` variable (MCH1202 at run time).
- Library names written in commands (QSYS, QTEMP, QGPL… are fine). A DCLF or INCLUDE turns the undeclared-variable check off, since they bring variables the source does not show.

## SQL checks

![SQL checks]({{ "/images/sql-checks.png" | relative_url }})
*SQL checks before you run a script.*

In SQL scripts (`vanthrex.lint.sql`) and in embedded SQL in RPG.

- UPDATE or DELETE without WHERE (quick fix in scripts: WHERE 1 = 1 when every row is meant), DROP / TRUNCATE flagged as irreversible, `= NULL` / `<> NULL` that is never true, SELECT INTO without WHERE (SQLCODE -811).
- Statements inside CREATE PROCEDURE / FUNCTION / TRIGGER are left alone; text in literals and comments is ignored.

## More snippets

 CL RCVF loop, DOWHILE, SELECT / WHEN / OTHERWISE, create-if-missing with CHKOBJ, OVRDBF … DLTOVR, SBMJOB, RTVJOBA, SUBR; SQL safe UPDATE (COUNT first), duplicate keys, table sizes, columns of a table, programs using a file.

## 7 checks on how variables are used

From their declared type, free and fixed form; also switched in `vanthrex.lint.rules`.

- `%SUBST` with a start or length beyond the field (RNX0100 at run time) and array indexes outside 1-DIM (RNX0121).
- Numeric literals too big for the field (`packed(5:2)` = 1234.5, `int(5)` = 40000) and text literals assigned to a number, with a quick fix that converts with `%DEC` / `%INT`.
- Numbers compared with `*BLANKS`, with a quick fix to compare with 0.
- SQL host variables (`:name`) that are not declared, with a quick fix that declares them with a type guessed from the name.
- `EXSR` of a subroutine that is not in the source, with a quick fix that creates the BEGSR … ENDSR.
- These checks stay silent when they cannot be sure: a /COPY, an EXTNAME / LIKEREC structure or a declared file may bring the name.

## More help while typing

- After `DCL-PI` in a procedure whose DCL-PR is already written, its parameters are suggested (and END-PI if missing); `WHEN` after `SELECT`; MONMSG after RCVF (CPF0864), RTVDTAARA / CHGDTAARA, CRTDTAQ, MOVOBJ and GRTOBJAUT.
- **Toggle Value** (Ctrl+Alt+Shift+T): `*ON` ↔ `*OFF`, `*YES` ↔ `*NO`, `AND` ↔ `OR`, `=` ↔ `<>`, `<` ↔ `>=`, `SETLL` ↔ `SETGT`, `READ` ↔ `READP`, `*START` ↔ `*END`… at every cursor, keeping the case.
- Very large sources (over 3 MB) keep the basic checks only, so the editor stays responsive.

## 6 checks for errors found late

Also switched in `vanthrex.lint.rules`.

- A DCL-PR that no longer matches the DCL-PI of its procedure (parameter count, types, CONST, return value), with a quick fix that updates the prototype from the interface.
- Calls with fewer arguments than the required parameters or more than the procedure has (`*NOPASS` understood, colons inside literals ignored).
- A CONST parameter that is changed, LEAVE or ITER outside a loop, DOW / DOU loops on a constant condition with no LEAVE or RETURN inside.
- Library names written in EXTFILE / EXTDESC / EXTNAME or in embedded SQL (QSYS2, SYSIBM, QTEMP… are fine).

## Modules and service programs

- **Generate Binder Source From the Exports**: STRPGMEXP with a named signature; an open binder source is updated in place, keeping its export order and adding new exports at the end.
- **Generate a Prototype Copybook From the Exports**: every exported procedure's DCL-PR, with a `/DEFINE` guard against a second /COPY.
- **Add a Header to Every Procedure** that has no comment above it, with its parameters and return value.
- **Join the Lines of a Statement** (the reverse of Wrap Long Line), refused when a `//` comment or a continued literal would break the code.
- **Remove Unused Declarations…**: one-line DCL-S / DCL-C never used, after a confirmation listing them (one Ctrl+Z restores them).
- 6 more snippets: `*PSSR`, procedure with ON-EXIT, array of data structures, GET DIAGNOSTICS, SET OPTION, DCL-ENUM.

## Robustness

- Each document is parsed once per change and shared by hints, completion, lenses, call hierarchy and the status bar; sources over 40,000 lines skip the per-line decorations.
- A provider that meets an unexpected source returns nothing instead of failing, and each group of checks runs on its own, so one never hides the others.
- Automatic END lines are never added during undo / redo, with several cursors, or when the line changed meanwhile.
- Snippet text (Surround With, call completion, headers) escapes `$`, `}` and `\`, so names like `$amount` stay intact.
- Format Embedded SQL keeps a comment after the `;`; Wrap Long Line works from the Problems view; the deprecated-opcode fix is offered only when the conversion is complete.

## Shortcuts

| Keys | Action |
|---|---|
| Ctrl+Alt+. | Close the open block |
| Ctrl+Alt+W | Surround With… |
| Ctrl+/ | Toggle RPG comment |
| Ctrl+Alt+PageDown / PageUp | Next / previous procedure |
| Shift+Alt+H | Call hierarchy |
| Ctrl+. | Quick fixes and refactorings |
| Ctrl+Alt+A | IBM i tools for this source |
| Tab | Accept the grey suggestion |
| Ctrl+Alt+Shift+T | Toggle value (*ON / *OFF, AND / OR…) |
