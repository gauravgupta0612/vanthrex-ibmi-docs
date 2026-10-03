---
layout: default
title: Your first connection
parent: Getting started
nav_order: 3
---

# Your first connection
{: .no_toc }

1. TOC
{:toc}

## Create the connection

1. Click the **Vanthrex** icon in the activity bar.
2. In the *Connections* view, click **+** (**Add IBM i Connection**).
3. Fill in the form:

| Field | What to enter |
|---|---|
| **Connection name** | Any label, for example *DEV400* |
| **Host name or IP** and **SSH port** | The IBM i address; port 22 unless your SSH server uses another |
| **User profile** | Your IBM i user profile |
| **Sign-in → Method** | *Password* (tick **Remember securely** to keep it in the VS Code secret store, never in settings) or *SSH private key* (click **Browse…** to pick the key file) |
| **Library list** | Your libraries, top first, separated by spaces or commas, for example `MYLIB APPLIB QGPL` |
| **Current library** | Where new objects go by default |
| **Compile objects into** | Optional: a development library that receives compiled objects. Empty = same library as the source |
| **Advanced → SQL engine** | Keep **Automatic (recommended)** |
| **Advanced → IFS start directory** | Optional start folder for the IFS browser (default: your home directory) |

4. Click **Test connection**. You'll see whether SSH works and which SQL engine will be used.
5. Click **Save connection**.

## Connect

Click the connection in the *Connections* view. The status bar shows the system name. Click it, or press **Ctrl+Alt+I**, at any time for the quick menu.

If the password isn't saved yet, you're asked for it and can choose to remember it securely.

{: .tip }
Set `vanthrex.autoConnectLast` to `true` to reconnect to the last system whenever VS Code starts.

## Your first five minutes

1. **Open a member.** Expand *Libraries & Source* → a library → *Source files* → `QRPGLESRC` → click a member. Each line shows its change date on the left.
2. **Edit and save.** Change a line and press **Ctrl+S**. The member is saved on the IBM i, and untouched lines keep their dates.
3. **Compile.** Press **Ctrl+Alt+C**. Errors appear underlined on the right line and in the *Problems* panel.
4. **Run SQL.** Open the quick menu (**Ctrl+Alt+I**) → **New SQL Scratchpad**, type `SELECT * FROM QSYS2.SYSTABLES FETCH FIRST 10 ROWS ONLY`, then press **Ctrl+Enter**.
5. **Check the system.** Click the dashboard icon on the *Connections* view.

## Create a new member

Right-click a source file → **New Member**. RPG and CL members start from a template that compiles as-is.

## Manage connections

Right-click a connection → **Edit** or **Remove**. Removing a connection also deletes its saved password.

**Next:** explore the [features](features.md).
