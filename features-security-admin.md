---
layout: default
title: "Security Admin"
nav_order: 23
parent: "Features"
---

# Security Admin and more (2.1)
{: .no_toc }

1. TOC
{:toc}

## Security Admin center (*SECADM)

**What it is:** User profile, group and authorization list administration in VS Code, for security administrators. It is visible only when your profile or one of its groups has *SECADM special authority.

**How:** Connections view toolbar → **Security Admin** (or the quick menu). From the list of profiles: **Create a user…**, **Copy a user…**, and per profile **Change attributes**, **Reset password**, **Enable / Disable**, **Expire password**, **Delete**. Reports: **Unused profiles** (with *Disable all*), **Powerful profiles**, **Group profiles**, **Authorization lists** (create, add / change / remove entries, objects secured). Every command is shown before it runs; passwords are masked everywhere. Changing the special authorities of other administrators may also need *ALLOBJ, as IBM i requires.

## Source and change tracking

- **Objects Out of Sync with Source** (right-click a library): compares the source date stored in each program, service program, module, command and file at compile time with the member's current date. "Source newer" means the object was not recompiled after the last change; "source missing" means it cannot be rebuilt.
- **What Changed (Release Notes)…** (right-click a library): members and objects changed in the last 1–90 days; **Copy as Markdown**.
- **New Member from Template…** (right-click a source file): eight built-in templates plus yours in `vanthrex.templates` (&NAME, &TEXT, &DATE, &USER are filled in).
- **Retrieve Binder Source** (right-click a service program) and **Work with Binding Directory** (right-click a *BNDDIR).

## Locks, SQL, exit points and bulk authority

- **Who Is Locking Rows?** (right-click a file): QSYS2.RECORD_LOCK_INFO with the job holding or waiting for each row.
- **Running SQL Statements** (Jobs view toolbar): statements running now, longest first; **Cancel** a runaway query.
- **Exit Points and Exit Programs** (quick menu or Security Admin): registered exit programs and unprotected network exit points.
- **Change Owner or Authority of Many Objects…** (right-click a library): change the owner of every object matching a generic name, or grant / revoke authority in one command.

## System, journals, IFS and message queues

- **Installed Software and License Keys**, **Is This PTF Installed?…** (quick menu).
- **Journals** (quick menu or right-click a library): receivers, size, objects journaled; change receiver; STRJRNLIB.
- **Permissions…** on an IFS file or folder: data authorities and owner, with changes for one object or a whole folder tree.
- **Work with Message Queue…**: any message queue — reply, remove, explain, sender's job log, send.

## Code and database quality

- **Compare Table Structure…** (right-click a file): columns and indexes against another library or another connected system, with an ALTER script for the second copy.
- **Find Unused Code** (right-click in an RPG editor): definitions nothing in the source refers to.
- **Find Hard-Coded Libraries** (right-click in an editor, or on a source file): library-qualified names in source; allow your shared libraries with `vanthrex.scan.allowedLibraries`.


## Jobs, history and dependencies

- **What Is This Job Doing?** (right-click a job, or quick menu): status, wait reason, current SQL, call stack, locks and activation groups in one page.
- **System History Log (QHST)…**: recent system messages by severity, message ID or text.
- **What Depends on This File?** (right-click a file): logical files, indexes, views, constraints, triggers and foreign keys.

## Source, IFS and network checks

- **Indicator Usage** (right-click in an RPG or DDS editor): where each indicator is set and tested; suspicious ones flagged.
- **Character Set (CCSID)…** on an IFS file or folder: see, tag or convert the CCSID.
- **Can the IBM i Reach This Host? (Ping)…** and **Call a Web API from the IBM i…**: test connectivity and REST services from the system itself.
