---
layout: default
title: "New in 3.1"
parent: "What's new"
nav_order: 1
---

# New in 3.1
{: .no_toc }

More power in the editor: DDS checks, CL formatting, RPG semantic highlighting, names edited together, END lines indented as you type, links to a line and clickable terminal output.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## What is new

![DDS checks while you type]({{ "/images/dds-checks.png" | relative_url }})
*DDS checks while you type: decimals, fields outside the screen, names declared twice, overlapping fields, missing lengths.*

![Format Document for CL]({{ "/images/cl-format-compare.png" | relative_url }})
*Format Document for CL puts labels, commands and parameters in the prompter columns and splits long commands with +.*


- **DDS checks while you type** (PF, LF, DSPF, PRTF; `vanthrex.lint.dds`): names longer than 10 characters, a field or record format declared twice, fields with no length (and no reference), more decimals than the length, lengths beyond the data type, key fields that are not in the record, display fields or constants outside the screen (DSPSIZ, *DS3 / *DS4) and display fields on top of each other. Reference fields, logical files and conditioned fields are left alone. DDS members are part of the Code Health Report too.
- **Format Document for CL** (Shift+Alt+F): the prompter layout — labels in column 1, commands in column 14, parameters from column 25, long commands split with `+` before column 80. Statements with a comment inside are kept as they are.
- **RPG semantic highlighting** (`vanthrex.editor.semanticHighlighting`): parameters, constants and CONST parameters (read-only), data structures and subfields, procedures, files and subroutines each get their own colour, and a global variable used inside a procedure is marked — on top of the existing syntax colours.
- **Names edited together**: renaming a procedure or a data structure on its `DCL-PROC` / `DCL-DS` line changes the name on its `END-PROC` / `END-DS` line at the same time, and the other way round.
- **END lines indented as you type** (`vanthrex.editor.indentOnType`): typing the `;` of ENDIF, ENDDO, ELSE, WHEN, OTHER, ON-ERROR, END-PROC… moves the line under its opener.
- **Links that open a member at a line**: *Copy a Link That Opens This Line* (right-click, or Ctrl+Alt+A → Copy) gives a `vscode://…` link for tickets, chats and e-mails; whoever clicks it, with Vanthrex installed, opens the same member (or IFS file) at the same line, on the named system after a confirmation.
- **Clickable IBM i references in every terminal** (`vanthrex.editor.terminalLinks`): `LIB/FILE(MEMBER)` opens the member, message IDs such as `CPF9801` or `MCH1210` are explained, IFS paths open the file — in the PASE terminal, build output, and any other terminal.

## Settings

| Setting | Default | What it does |
|---|---|---|
| `vanthrex.lint.dds` | on | DDS checks while you type |
| `vanthrex.editor.semanticHighlighting` | on | RPG names coloured by what they are |
| `vanthrex.editor.indentOnType` | on | END / ELSE / WHEN lines moved under their opener |
| `vanthrex.editor.terminalLinks` | on | Members, message IDs and IFS paths clickable in terminals |

Each DDS check can also be turned off in `vanthrex.lint.rules`.
