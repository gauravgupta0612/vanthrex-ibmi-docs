---
layout: default
title: "Operations"
nav_order: 18
parent: "Features"
---

# Operations
{: .no_toc }

Storage & cleanup advisor, live alerts, message files, field finder and object promotion — new in 1.0.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Storage & cleanup advisor

**What it is:** For your library list, one library or all user libraries: libraries and objects by size, objects not used for a chosen number of days, files with many deleted rows, saved journal receivers older than 30 days, and old spooled files by user — with how much space each could free. **IFS folders by size** measures a folder tree in the IFS.

**How:** Quick menu → **Storage & cleanup advisor…**, or right-click a library. Click a row for its options: reorganize a file (RGZPFM), delete a receiver or an unused object, delete a user's old spooled files. Nothing is deleted without asking.

## Live alerts

**What it is:** Notifications in VS Code when a job waits for a reply (MSGW), an inquiry message arrives on QSYSOPR, a batch job ends abnormally (end code 10 or more), or the system ASP passes the alert level.

**How:** *Jobs* view toolbar → **Live Alerts** → *Turn on* (or set `vanthrex.alerts.enabled`). Reply to an inquiry or open the job log right from the notification. `vanthrex.alerts.scope` chooses your own jobs or all users, `vanthrex.alerts.intervalSeconds` how often to check, `vanthrex.alerts.diskPercent` the disk level.

## Message files and field finder

- **Message files:** right-click a `*MSGF` → **Work with Message Descriptions**: add (the next free ID is proposed), change, copy as ADDMSGD or remove messages.
- **Field finder:** quick menu → **Field finder…**, type a field name (wildcards * and % allowed) and pick the libraries; optionally search descriptions and headings too. Fields with the same name but different definitions are flagged. Click a result to see the programs using that file.

## Object promotion (DEV → TEST → PROD)

**What it is:** Copies objects from one library to another the safe way: compare first, back up what will be replaced, copy with SAVOBJ / RSTOBJ (attributes and authorities come along), and log it.

**How:** Right-click an object or a library → **Promote Objects…**, pick the objects and the target library. The compare page warns about objects that are newer in the target and physical files that carry data; **Promote** shows every command before it runs. **Promotion log** lists every promotion with its backup save file and an **Undo**. The backup library is `vanthrex.promotion.backupLibrary` (QGPL by default).

