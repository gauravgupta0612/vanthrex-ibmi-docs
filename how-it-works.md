---
layout: default
title: How it works
nav_order: 6
---

# How it works
{: .no_toc }

What happens on the IBM i when you use Vanthrex. Useful for system administrators and for understanding error messages.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Architecture

```
VS Code (your PC)
  └─ Vanthrex extension
       ├─ SSH session ──► QSH / PASE: CL commands, file transfer (SFTP), compile
       └─ SQL engine
            ├─ Mapepire over SSH  (JAR in ~/.mapepire, started inside the SSH session)
            ├─ Mapepire daemon    (port 8076, certificate checked)
            └─ db2util            (fallback, run over SSH)
```

Only one connection is active at a time. Nothing runs on the IBM i when you are disconnected.

## Opening and saving members

**With a Mapepire SQL engine** (the default):

- **Read:** Vanthrex creates a temporary alias in `QTEMP` over the member and reads it with SQL in relative-record order, including `SRCSEQ` and `SRCDAT` for every line.
- **Save:** your lines are compared with the original (line diff). Untouched lines keep their date, changed and new lines get today's date, and sequence numbers are reassigned.
- The new content is written to a work table in `QTEMP`, the member is backed up, then replaced with `CPYF MBROPT(*REPLACE) FMTOPT(*MAP)`. If the replace fails, the backup is copied back.
- Saves to the same member are queued, so two quick saves can't overlap.

**With db2util:** members are copied with `CPYTOSTMF` / `CPYFRMSTMF` in CCSID 1208 (UTF-8) through `vanthrex.tempDirectory`. Dates are reset on save.

Text is transferred as UTF-8, so national characters survive the round trip.

## Locks and conflicts

- Before opening and saving, Vanthrex reads `QSYS2.OBJECT_LOCK_INFO` for the member and the change timestamp of the member.
- The lock banner shows the job, user (with their name from `QSYS2.USER_INFO`) and lock state.
- **Ask to release** sends `SNDBRKMSG` (or `SNDMSG` to their message queue). **Notify me when free** checks every 15 seconds for up to 30 minutes. **End their job** runs `ENDJOB` after you confirm.

## Running CL

Each command runs in a QSH job whose library list is set from the connection (`liblist`), then `system "<command>"`. Interactive (5250) commands can't run this way.

## Compiling

The compile action's command is filled in with `&LIB`, `&OBJLIB`, `&NAME` and the other variables, then run like any CL command. Errors are read from `&OBJLIB/EVFEVENT(&NAME)` and shown in the editor and the *Problems* panel. For SQLRPGLE, errors the RPG compiler reports on the precompiled source are shown on line 1 with the generated line number.

## CL prompter

F4 on a CL command calls the `QCDRCMDD` API to get the command's real definition (XML) from the IBM i, then builds the form from it. It works for IBM and your own commands.

## SQL services used

The dashboard, jobs, messages and search features use standard IBM i Services, including `SYSTEM_STATUS_INFO`, `ACTIVE_JOB_INFO`, `JOBLOG_INFO`, `MESSAGE_QUEUE_INFO`, `OBJECT_STATISTICS`, `OBJECT_LOCK_INFO`, `GROUP_PTF_INFO`, `SYSTABLES`, `SYSCOLUMNS` and `SPOOLED_FILE_DATA`.

## What is stored on your PC

| What | Where |
|---|---|
| Connection profiles | VS Code global state |
| Passwords | VS Code secret store (Windows Credential Manager, macOS Keychain, libsecret) |
| Local history of members and IFS files | VS Code's extension storage folder |
| Settings | Normal VS Code settings |
