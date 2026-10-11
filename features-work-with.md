---
layout: default
title: "Work with… (WRK screens)"
nav_order: 17
parent: "Features"
---

# Work with… (WRK screens)
{: .no_toc }

Subsystems, job queues, output queues, job scheduler, user profiles, system values, the security audit journal, save files and TCP/IP — new in 0.11.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

Open any of them with **IBM i: Work with…** (quick menu, the *Jobs* view toolbar, or right-click the active connection). Click a row for its options. Every command is shown before it runs.

## Work management

**What it is:** Subsystems (WRKSBS), job queues and their waiting jobs (WRKJOBQ), output queues and their spooled files (WRKOUTQ), and job schedule entries (WRKJOBSCDE).

**How:** **IBM i: Work with…** → pick a screen. Click a row for its options: start / end a subsystem, hold / release / clear a queue, release / hold / run next / end a waiting job, open / hold / release / move / delete a spooled file, add / hold / release / remove a schedule entry. Every command is shown before it runs, with **Copy Command** as an alternative.

## Users & security

- **User profiles** (WRKUSRPRF): filter non-IBM, disabled, with special authorities, or group profiles; enable, disable, expire the password (passwords are never shown or set); see the user's active jobs and owned objects.
- **System values** (WRKSYSVAL): all of them, read-only, with the important ones grouped and explained.
- **Security audit journal** (QAUDJRN): pick event types (authority failures, invalid passwords, profile and system value changes, deleted objects…), a time range and optionally a user. Needs *AUDIT or *ALLOBJ.

## Save / restore

**What it is:** Save files in a library (WRKSAVF) and their contents; save a library or objects to a save file (SAVLIB / SAVOBJ, target release, compression, run now or submit to batch); restore everything or some objects, also into another library (RSTLIB / RSTOBJ); download a save file to the PC or upload one.

**How:** Right-click a library → **Work with Save Files** / **Save Library or Objects…**, or right-click a save file → **Show Save File Contents**. Listing contents needs IBM i 7.4 with recent Db2 PTF groups.

## Network & services

**What it is:** TCP/IP connections with the job and user behind each, and listening ports (NETSTAT); the common TCP/IP servers with their status and start / end (STRTCPSVR / ENDTCPSVR, STRHOSTSVR); IP interfaces and routes.

**How:** **IBM i: Work with…** → *TCP/IP connections*, *TCP/IP servers* or *IP interfaces*. Ending SSHD or your own connection disconnects Vanthrex — you are warned first. Starting and ending servers needs *IOSYSCFG.

These screens need a Mapepire SQL connection and IBM i Services (IBM i 7.4 or later recommended). What you can do depends on your own authorities — Vanthrex never goes beyond them.
