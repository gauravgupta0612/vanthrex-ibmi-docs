---
layout: default
title: "Create & check (2.3)"
nav_order: 26
parent: "Features"
---

# Create & check (2.3)
{: .no_toc }

Create a library or an IFS folder from anywhere, grade your RPG sources, take a library list from a job description, find objects open to everybody and compare two systems.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

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
