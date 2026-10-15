---
layout: default
title: "System Tracker"
nav_order: 25
parent: "Features"
---

# System Tracker (2.2)
{: .no_toc }

The whole IBM i in one page: what needs attention, every library, jobs, storage, messages, users, PTFs and your own work — with an action on every row.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## How to open it

- The **pulse** button at the top of the Connections view, or the inline button on the active connection.
- **Ctrl+Alt+T** (Cmd+Alt+T on a Mac), or the quick menu (Ctrl+Alt+I) → *System Tracker*.

## Tabs

| Tab | What you see | What you can do |
|---|---|---|
| Overview | **Health score** (0–100, ✓ / ⚠ / ✗) with the reasons that lowered it and its trend; system and release, CPU, system ASP use, jobs, waiting jobs, QSYSOPR replies, time since IPL, PTF level, libraries, your compile results — and **Needs attention** | Click a tile or an alert to go where it is fixed; PDM, Find member, Performance monitor, Running SQL, QHST, Exit points |
| Libraries | Every library (all of them with *ALLOBJ): type, text, owner, created, last used, place in your library list; objects and size on request (remembered); tiles for user / TEST libraries, missing library-list entries, libraries not used for a year and your special authorities | Filter, sort, hide IBM libraries, only my library list, not used for a year; open in PDM, add to the library list, pin, storage advisor; export CSV |
| Jobs | Waiting jobs (MSGW, LCKW), top jobs by CPU, subsystems with status and maximum jobs | Details, job log, live job log |
| Storage | System ASP use, size and free space, largest libraries (measured), auxiliary storage pools | Library sizes |
| QSYSOPR | Latest messages, inquiries highlighted | Explain, the sender's job log, work with QSYSOPR (reply, remove) |
| Users | Security system values (QSECURITY, QPWDLVL, QMAXSIGN, QPWDEXPITV, QPWDMINLEN, QAUDCTL, QCRTAUT, QINACTITV, QALWOBJRST) with advice; profiles enabled / disabled, not signed on for 90 days, expired passwords, failed sign-on attempts, *ALLOBJ and *SECADM profiles | Security Admin (for *SECADM users) |
| Queues | Job queues (stuck ones flagged: held, or not attached to a subsystem, while jobs wait), output queues by number of spooled files | Hold / Release (asked first) |
| Network | Listening ports and their services, open connections, unencrypted services, the busiest remote addresses | — |
| Scheduled jobs | The job schedule, next run first; today's runs highlighted, held entries flagged | Hold / Release (asked first) |
| Journals | Journals in user libraries, largest first: attached receiver, receivers kept, size, journaled objects; 50+ receivers or 10 GB+ flagged | Work with the journals of that library |
| What changed | On request: objects changed today or in 7 days, or the largest objects — library list (fast) or all user libraries (slow) | Information, PDM, locks |
| All systems | Every connected system side by side: health, CPU, ASP, MSGW, QSYSOPR replies | Open (switch to it) |
| PTFs & software | Release, cumulative PTF and TR level, all installed PTF groups | Installed software and license keys, "Is this PTF installed?" |
| My work | Your jobs, spooled files, members changed in your library list in the last 7 days, broken compiles, pins | Open, PDM, compile history |

## Health score

Starts at 100; each problem costs points — disk 80 % / 90 % / 95 %, messages waiting for a reply, MSGW and LCKW jobs, CPU over 90 %, QSECURITY below 40, risky security values, failed compiles, missing library-list entries, expired passwords. 85+ is healthy, 60–84 keep an eye on it, below 60 action needed. CPU, ASP, jobs and the score keep their history between refreshes and show a trend line. **Copy summary** puts a short Markdown report on the clipboard.

## Save report

**Save report** (header) writes the whole tracker — every tab — as one HTML page in a light theme that prints well: send it to your team, attach it to a ticket or keep it as a record of the system on that day.

## Good to know

- Each part is read on its own: if an IBM i service does not exist on your release or you are not authorized to it, that part says why and the rest of the page still works.
- Library sizes use `QSYS2.LIBRARY_INFO`, four libraries at a time, only when you ask — on a big system that takes a while. Filter first to size only what you need.
- *Users* shows the profiles you are authorized to see; with *SECADM you see them all.
- *Libraries* lists the libraries you are authorized to; *ALLOBJ lists every library (*SECADM manages profiles, not objects).
- Every table has **Export CSV**; tick **Refresh every minute** in the header to keep the page current.
