---
layout: default
title: Why Vanthrex
nav_order: 2
---

# Why Vanthrex
{: .no_toc }

1. TOC
{:toc}

## The problem

IBM i development usually means switching between several tools: a 5250 session for SEU and PDM, spooled files to read compile errors, a separate SQL client, DFU for data, and green-screen commands to check the system.

## What it replaces

| Task | Traditional way | With Vanthrex |
|---|---|---|
| Edit source | SEU / PDM in a 5250 session | VS Code editor with colours, outline, F12 / F2 |
| Compile | `WRKMBRPDM` option 14, then read the spool file for errors | **Ctrl+Alt+C** → errors underlined on the right line |
| Run SQL | STRSQL or a separate SQL client | **Ctrl+Enter** → sortable grid, CSV export, autocomplete |
| Look at data | UPDDTA / DFU / a query | **Edit Table Data** grid |
| Check the system | WRKACTJOB, WRKSYSSTS, DSPMSG QSYSOPR | **System Dashboard**, *Active Jobs* and *Messages* views |
| Find code | `FNDSTRPDM`, DSPPGMREF printouts | **Ctrl+Alt+F**, **Ctrl+Alt+O**, **Where Used** |
| Undo a mistake | Hope someone kept a backup | **Local History** on every open and save |
| See what changed when | SEU date column | **Source dates** in front of every line, kept on save |
| Someone else has the member | "Member in use" error, then WRKOBJLCK | **Lock banner** with the person's name and *Ask to release* |

It is built for people who are **new to IBM i** (guided forms, templates, plain-language messages) as well as **experienced developers** who want speed and modern tooling.

## Why it is powerful

- **Nothing to install on the IBM i.** It only needs SSH. Fast SQL ("Mapepire") is uploaded and started automatically, and needs only Java, which IBM i already has.
- **Safe by default.** It asks before risky SQL (DROP, DELETE without WHERE), before deleting objects or ending jobs, and before writing table data. Passwords go in the VS Code secret store, never in settings files.
- **Never lose work.** Every member you open or save is copied locally, so you can compare and restore any version. Member saves are staged and replaced in one step, with an automatic restore if the replace fails.
- **Understands RPG.** It knows declarations, procedures, /COPY members and fixed-format columns, so navigation, rename and checks work on real code.
- **Respects SEU habits.** Source dates and sequence numbers are kept, F4 prompts specs, and locks are shown with a name instead of a cryptic error.
- **Clear when something goes wrong.** Errors appear inline or as clear messages, and every command sent to the IBM i is written to an output log you can read.
- **Configurable.** Compile commands, checks, page sizes and refresh times are ordinary VS Code settings.

## Who it is for

- **RPG, CL and SQL developers** moving from SEU/PDM or RDi to VS Code.
- **Teams** that share source files and need to see who is working on what.
- **Newcomers to IBM i**, who get forms and templates instead of command syntax to memorise.
- **Operators and leads** who want a quick view of jobs, messages and system health.
