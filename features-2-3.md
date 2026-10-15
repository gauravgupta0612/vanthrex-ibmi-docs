---
layout: default
title: "New in 2.3"
nav_order: 26
parent: "Features"
---

# New in 2.3: create, check and stay connected
{: .no_toc }

Stay connected when the network drops, create a library or an IFS folder from anywhere, grade your RPG sources, take a library list from a job description, find objects open to everybody and compare two systems.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Stable connections

| What happens | What Vanthrex does |
|---|---|
| The network, VPN or laptop sleep drops the connection | Reconnects by itself with the saved sign-on: 5 attempts over about 2 minutes, shown in the status bar; the system becomes active again. Turn off with `vanthrex.connections.autoReconnect`. |
| The system stops answering but SSH did not notice | Every minute (`vanthrex.connections.healthCheckSeconds`) a tiny query checks it; a slow answer shows its time in the status bar, two misses in a row reconnect. *Check Connection Health* and *Reconnect Now* are on the active connection. |
| You save while the connection is gone | The change is kept on this computer and offered for saving when the system is back (*Save Now*, *Show*, *Discard*); *Changes Kept While Offline…* lists them. |
| VS Code restarts with member or IFS tabs open | The tabs that could not be read reopen by themselves once you are connected. |
| You disconnect with unsaved members | You are asked: *Save and Disconnect* or *Disconnect Anyway*. |

## Copy to Another System

With two systems connected, right-click a member or an IFS file (or use the editor menu) → *Copy to Another System…*. Pick the target system and name; the source file and member are created when missing, and you see how many lines would change before anything is written. A protected system still asks before the change.

## Call a program with typed parameters

Right-click a program → *Call Program (Typed Parameters)…* (also PDM option 16). Vanthrex finds the program's source (through its entry module for ILE programs), reads its parameter list — free-form `dcl-pi`, fixed `D … PI`, `*ENTRY PLIST`, or `PGM PARM(…)` in CL — and asks for each value with its type, checking it as you type.

| Parameter | What a plain CALL passes | What Vanthrex passes |
|---|---|---|
| packed(9:2), value -12.5 | packed(15,5) — the program reads garbage | `X'000001250D'` |
| zoned(5:2), value -1.23 | packed(15,5) | `'0012L'` |
| int(10), value 42 | packed(15,5) | `X'0000002A'` |
| char(50), value `ABC` | 32 bytes — the rest is whatever follows | `'ABC'` padded to 50 |

Then run it, submit it to batch, or copy the command. Your last values are remembered per program. When the source cannot be found, describe the parameters yourself.

## Who is signed on

Jobs view toolbar, quick menu or System Tracker: every 5250 session (user, job, subsystem, status, what it is doing) and the server connections per user (ODBC/JDBC, file server, remote command, SSH…). Click a session for details, its job log, a break message, or to end it (controlled or immediately — asked first). *Message everyone signed on* sends a break message to every session.

## Member notes

Right-click a line in a member → *Add Note to This Line*. Notes appear at the end of the line and as a *📝 N notes* lens at the top of the member; they follow their line when code moves. *Notes on This Member* and *All Member Notes…* list them. To share notes with your team, set `vanthrex.notes.sharedFile` to an IFS file everybody can read and write (for example `/home/TEAM/vanthrex-notes.json`).

## Create Library

Libraries view toolbar, quick menu (Ctrl+Alt+I), System Tracker, or F6 on the PDM library screen. Four short steps: name, text, *TEST or *PROD, and what else to do at the same time — add it to your library list, make it your current library, and create the usual source files (QRPGLESRC, QCLLESRC, QDDSSRC, QSQLSRC, QCPYSRC, QSRVSRC, QCMDSRC, record length 112). At the end you can open it in PDM.

## Create IFS folder or file

IFS view toolbar, right-click a folder, quick menu or System Tracker. Type the full path; missing parent folders are created. New files are tagged UTF-8 (CCSID 1208) and opened in the editor. You can set permissions (for example 755 or 644).

## Source Quality Report

Right-click a source file → *Source Quality Report*. Every RPG member is read and scored:

| Measure | Why it matters |
|---|---|
| Code check findings (errors, warnings) | The same checks as in the editor |
| Fixed-format share | How much is left to convert to free format |
| Numbered indicators | Hard to read and to change |
| GOTO / CABxx | Jumps make the flow hard to follow |
| Subroutines and procedures | How the program is structured |

Score: 100 minus errors, warnings per 1,000 lines, GOTOs, numbered indicators and the fixed-format share. Grades: A 90+, B 75+, C 60+, D 40+, E below 40. The lowest scores come first, and the report lists the most frequent findings for the whole source file.

## Library list from a job description or user profile

Libraries view (… menu), right-click the active connection, or the System Tracker. Pick a user profile (its job description is used) or a job description; you see what would be added and removed, then replace your library list or add only the missing libraries. *SYSVAL follows the QUSRLIBL system value.

## *PUBLIC Authority Scan

Right-click a library, or *PUBLIC on a library in the System Tracker. Objects that give *ALL or *CHANGE to *PUBLIC come first; click one to set *PUBLIC to *USE (asked first). Some objects need more than *USE on purpose — check that programs and users still work.

## Compare System Values

With two systems connected: Connections view (… menu) or the *All systems* tab of the System Tracker. Values that differ come first; values that differ on purpose (dates, serial numbers, devices) are listed apart.
