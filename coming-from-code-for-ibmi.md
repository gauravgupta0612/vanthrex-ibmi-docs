---
layout: default
title: "Coming from Code for IBM i"
parent: "Getting started"
nav_order: 4
---

# Coming from Code for IBM i
{: .no_toc }

Bring your connections, library lists and compile actions into Vanthrex in one step — and share one setup with your whole team.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Import your setup

1. Open the command palette (`Ctrl+Shift+P`) and run **Import My Code for IBM i Setup (Connections, Library Lists, Actions)…**
2. Choose what to import:
   - **Connections**: host, port, user and SSH key. Passwords are never read: you type each one at the first connection.
   - **Library lists**, current library and home folder; library list profiles become Vanthrex *library list sets*.
   - **Compile actions** from your settings and from the workspace `.vscode/actions.json`. Variables such as `&OPENLIB`, `&OPENSPF`, `&OPENMBR` and `&BUILDLIB` are converted.
3. Connect and work. Both extensions can stay installed while you try Vanthrex.

## Keep your coding rules

Run **Import Coding Standards from rpglint.json…** to turn the rules your team already uses into Vanthrex [team coding standards](features-3-0.md#everything-in-vanthrex-for-one-person-or-a-whole-team), checked while you type.

![Team coding standards]({{ "/images/team-standards.png" | relative_url }})

## Share one setup with the team

**Export a Team Setup File…** writes the connections (without user names, passwords or key paths), library list sets, CL macros, compile actions, checks, team standards and AI privacy settings to one JSON file. A colleague runs **Import a Team Setup File…**, types their user profile once and works with the same setup.

## What you get on top

- More than 50 [checks while you type](features-rpg-checks.md) for RPG, CL and SQL, most with a quick fix, and [suggestions while you type](features-2-6.md#suggestions-while-you-type).
- [PDM in one screen](features-pdm.md), AS/400 [GO menus](features-3-0.md) and SEU-style [source dates and F4 prompters](features-seu-editing.md).
- The [Developer Toolbox](features-2-6.md#developer-toolbox) (`Ctrl+Alt+A`), a [call graph](features-call-graph.md), a [code health report](features-3-0.md) of whole libraries, and the [AI assistant](features-ai.md).
