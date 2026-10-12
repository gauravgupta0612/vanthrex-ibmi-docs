---
layout: default
title: "Safe on production"
nav_order: 20
parent: "Features"
---

# Safe on production
{: .no_toc }

Production and read-only protection, a self-check of the system, and errors that explain what to do — new in 1.2.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Production protection

**What it is:** Per connection: *No protection*, *Production: ask before every change*, or *Read-only: never change anything*. Covers CL commands, SQL that changes data or objects, member saves and IFS writes; reading, querying, downloading and Vanthrex's own work in QTEMP are never blocked.

**How:** In the connection form under **Protection**, or right-click a connection → **Set Protection…**. The status bar shows 🛡 (production, red) or 🔒 (read-only, amber).

## Self-check and plain-language errors

- **Self-check:** quick menu or right-click the active connection → **Self-Check**. Checks SSH and SQL latency, QSH/CL, the SQL engine and Java, CCSID, home directory, library list, release and Db2 PTF group, special authorities, RPGUnit and the debug service, and which IBM i services are missing (with the features they affect). **Copy the report** for a support issue. Runs automatically the first time you connect to a system in a session (`vanthrex.selfCheck.onConnect`).
- **Errors explained:** every error from IBM i, Db2 or SSH ends with what to do next (missing service → PTF group, not authorized → Check Authority, SQL7008 → WITH NC, locks → Who Has It Locked?, lost connection → reconnect…).

