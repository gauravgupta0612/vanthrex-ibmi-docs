---
layout: default
title: "System tools"
nav_order: 16
parent: "Features"
---

# System tools
{: .no_toc }

Journal explorer, authority checker, data queues & data areas, and the PTF & system health report — new in 0.9.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Journal explorer — who changed this table?

**What it is:** The row changes recorded in the journal for one table: which rows were added, updated or deleted, when, by which user, from which program and job — with the before and after record images of an update side by side, and a summary of who changed the table most.

**Why it helps:** "Who changed this customer's balance yesterday?" usually means DSPJRN to an outfile and a home-made query. Here it is one right-click.

**How:** Right-click a file → **Journal Explorer: Who Changed This Table?**, pick a time range (last hour to last 30 days) and optionally a user. Click a change to see the full history of that row (by relative record number). If the file is not journaled, Vanthrex says so and offers the `STRJRNPF` command. Uses `QSYS2.DISPLAY_JOURNAL`; before images need `IMAGES(*BOTH)`.

## Authority checker

**What it is:** Answers "can user X use this object, and if not, why not?" It resolves the user's authority the way IBM i does — *ALLOBJ, the user's own authority, group profiles, authorization list, *PUBLIC — checks *EXECUTE on the library too, and lists everyone with authority on the object.

**Why it helps:** "Not authorized" errors (CPF9802, CPF2189, SQL0551) are slow to untangle by hand with DSPOBJAUT, DSPUSRPRF and DSPAUTL. You get the exact source of the authority, what is missing, and the fix.

**How:** Right-click any object → **Check Authority…**, enter the user and what they need to do (use, change data, manage). If something is missing, **Grant…** shows the `GRTOBJAUT` command to run or copy. Adopted authority is not taken into account.

## Data queues and data areas

- **Data queues:** right-click a `*DTAQ` → **View Data Queue Entries** to peek at the waiting entries (data, key, sender job and user, time) without removing them. **Send a test entry…** and **Clear all entries…** are on the page (both ask first).
- **Data areas:** right-click a `*DTAARA` → **View Data Area** (type, length, value by position) or **Change Data Area Value…** — the new value is checked against the type, length and decimals before `CHGDTAARA` runs.

## PTF & system health

**What it is:** One report with the release, system ASP use, PTF groups compared with the latest levels at IBM, PTFs waiting for an IPL or loaded but not applied, certificates expiring within 60 days, user profiles with default passwords or passwords about to expire — ranked worst first with what to do.

**Why it helps:** These are the things that cause outages and audit findings, and they live in five different places.

**How:** Quick menu → **PTF & system health**, or right-click the active connection. Nothing is changed. The IBM comparison (`SYSTOOLS.GROUP_PTF_CURRENCY`) needs internet access from the IBM i; certificate and default-password checks need *ALLOBJ and *SECADM. Checks that can't run are listed as *not checked*.

All four need a connection with the Mapepire SQL engine and IBM i Services (IBM i 7.4, or 7.3 with recent Db2 PTF groups). They only read, except where a button says otherwise — and those always ask first.
