---
layout: default
title: Roadmap
nav_order: 11
---

# Roadmap

What is planned next. Ideas and votes are welcome in [GitHub issues](https://github.com/gauravgupta0612/silverlake-ibmi/issues/new/choose).

## Next

- **Service entry points** for the debugger (stop when any job calls the program).
- **AI: inline suggestions** while typing RPG, and an AI-written summary on the object information page.
- **Git: branch per library** (for example `dev` ↔ DEVLIB, `main` ↔ PRODLIB) and a pull-request check that compiles changed members.

## Later

- Parameters for *Extract to procedure*.
- I and O specs in the fixed → free converter.
- Call graph across systems (compare DEV and PROD references).

## Done

- **0.6.0** — AI assistant (`@vanthrex`) with IBM i tools for Copilot agent mode, Git for IBM i source, call graph & impact analysis, several systems at once, SQL Explain, and H/F/D/P specs in the fixed → free converter.
- **0.5.0** — IBM i debugger (batch debug with breakpoints, variables and call stack) and a debugger setup check.
- **0.4.0** — object information, object locks, compare libraries, modules & exports, generate DDL, run SQL scripts, SQL history and saved queries, prototype generation, extract to procedure, /COPY usage check, and a fix for members that could not be opened.
- **0.3.1** — documentation site and *Open Documentation* command.
- **0.3.0** — SEU-style source dates, F4 prompters, lock banner and conflict protection, member list with dates.
