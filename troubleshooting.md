---
layout: default
title: Troubleshooting
nav_order: 7
---

# Troubleshooting
{: .no_toc }

1. TOC
{:toc}

## First step: read the log

Open **View → Output** and choose **Vanthrex for IBM i** in the drop-down. Every command sent to the IBM i and every message that comes back is written there. Most error pop-ups also have a **Show Log** button.

## Connecting

### "Could not connect to *host*"

- Check that the SSH server is running on the IBM i: `STRTCPSVR SERVER(*SSHD)`.
- Check that port 22 (or your SSH port) is open between your PC and the IBM i. From a terminal: `ssh MYUSER@myibmi`.
- Wrong password saved? Choose **Forget Saved Password** in the error message and connect again.
- Key sign-in: the key file must be in OpenSSH format and its public key must be in `~/.ssh/authorized_keys` on the IBM i. The home directory and `.ssh` must not be writable by others.

### "Connection to *name* was closed"

The SSH session ended (network drop, the job was ended, or the system restarted). Click **Reconnect**.

### Commands are "not found" or nothing happens when clicking

The extension may have started with an error. Look for a message *"Vanthrex started with problems"* and click **Show Log**. Reload the window (**Ctrl+Shift+P** → *Developer: Reload Window*). If you also have the old *Silverlake* extension installed, uninstall it.

## SQL

### "No SQL engine could be started"

Vanthrex tried every engine and lists why each failed:

| Message | Fix |
|---|---|
| *Java was not found on the IBM i (install 5770-JV1)* | Install the Java licensed program, or pick another engine |
| *db2util is not installed (yum install db2util)* | Install it with `yum`, or use Mapepire |
| *the Mapepire daemon needs password authentication* | Use password sign-in, or switch to *Mapepire over SSH* |

With **Mapepire over SSH**, the first connection uploads the server JAR to `~/.mapepire`. Your home directory must exist and be writable.

### "Where-used needs the Mapepire SQL engine"

*Where used*, source dates and conflict checks need Mapepire (over SSH or daemon). Edit the connection → **Advanced** → **SQL engine** → *Automatic* or *Mapepire over SSH*.

### A statement asks for confirmation

`DROP`, `TRUNCATE`, and `DELETE` / `UPDATE` without `WHERE` always ask first. Turn this off with `vanthrex.sql.confirmDestructive` (not recommended).

## Editing members

### "The editor could not be opened due to an unexpected error"

This happened in 0.3.x with the Mapepire SQL engine (the output log shows *Result set was null*). **Update to 0.4.0 or later**: the problem is fixed, and if reading a member with source dates ever fails, the member now opens without dates instead.

### "Saving *LIB/FILE(MBR)* failed — the previous version was put back"

The member is replaced in one step from a copy staged in QTEMP. When that fails, the backup is restored, so nothing is lost. Common causes:

- A line is **longer than the source file's record length** (for example more than 80 characters in a 92-byte QRPGLESRC). Shorten it, or use a source file with longer records.
- A character can't be converted to the source file's CCSID.
- The member is locked by another job — see below.

### "Member in use" / the member is locked

The lock banner at the top of the editor shows who has it. Use **Ask to release**, **Notify me when free**, or (with `*JOBCTL`) end their job.

### The editor says the member changed on the IBM i

Someone saved the member after you opened it. Choose **Compare First** to see their change, then merge it, or **Overwrite** if you're sure.

### Source dates are not shown

Source dates need a Mapepire SQL engine and `vanthrex.sourceDates.enabled = true`. Press **Ctrl+Alt+D** to cycle the display if it was hidden.

## Compiling

### Errors aren't shown inline

The compile command must include `OPTION(*EVENTF)`; Vanthrex reads the errors from `&OBJLIB/EVFEVENT(&NAME)`. All built-in actions include it. Check your own entries in `vanthrex.compileActions`.

### Wrong object library

Set **Compile objects into** in the connection form, or use `&OBJLIB` in your compile command.

## Still stuck?

[Open an issue](https://github.com/gauravgupta0612/silverlake-ibmi/issues/new/choose) with the lines from the output log (remove host names and user names you don't want to share).
