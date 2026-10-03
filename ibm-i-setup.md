---
layout: default
title: IBM i setup
parent: Getting started
nav_order: 2
---

# IBM i setup
{: .no_toc }

Vanthrex needs **nothing installed** on the IBM i beyond what most systems already have.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## 1. SSH server (required)

Everything goes through SSH: browsing, transfers, CL commands and SQL.

```
STRTCPSVR SERVER(*SSHD)
```

To start it automatically after an IPL:

```
CHGTCPSVR SVRSPCVAL(*SSHD) AUTOSTART(*YES)
```

Your user profile needs a **home directory** in the IFS (for example `/home/MYUSER`). If it doesn't exist, create it:

```
MKDIR DIR('/home/MYUSER')
CHGUSRPRF USRPRF(MYUSER) HOMEDIR('/home/MYUSER')
```

## 2. An SQL engine (strongly recommended)

SQL powers the result grid, autocomplete, the dashboard, jobs and messages views, source dates and lock information. In the connection form, keep **SQL engine = Automatic** and Vanthrex tries these in order:

| Engine | What it needs | Notes |
|---|---|---|
| **Mapepire over SSH** | **Java** (licensed program 5770-JV1; a current JDK such as 11 or 17 is recommended) | Best choice. Nothing to install: Vanthrex uploads the Mapepire server JAR to `~/.mapepire` on first use and runs it inside your SSH session. It picks the newest 64-bit JDK it finds. |
| **Mapepire daemon** | A Mapepire server already running (port 8076) | Use when your administrator runs Mapepire as a service. The server certificate is checked on connect. |
| **db2util** | `yum install db2util` (open-source package) | Fallback. Source dates, conflict checks and *Where used* are not available with db2util. |

Check that Java is installed:

```
QSH CMD('ls /QOpenSys/QIBM/ProdData/JavaVM')
```

## 3. Authorities

| To use… | You need |
|---|---|
| Browse, edit, compile | Normal authority to the libraries and source files |
| End another user's job (lock banner, Active Jobs) | `*JOBCTL` special authority |
| Reply to QSYSOPR messages | Authority to the QSYSOPR message queue |
| Dashboard and IBM i Services | Authority to the QSYS2 services (most are `*PUBLIC *USE`) |

## 4. Network

- Port **22** (or your SSH port) must be reachable from your PC.
- Port **8076** only if you use a Mapepire daemon.

**Next:** [Your first connection](first-connection.md)
