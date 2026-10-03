---
layout: default
title: "System, jobs & messages"
nav_order: 8
parent: "Features"
---

# System, jobs & messages
{: .no_toc }

Dashboard, active jobs, message replies, the CL runner and spooled files.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## System dashboard

**What it is:** A live page showing:

- CPU, system ASP, job counts and memory
- the top jobs by CPU
- the latest QSYSOPR messages
- installed PTF group levels

**Why it helps:** It answers "is the system OK?" in one glance instead of three green-screen commands.

**How:** Click the dashboard icon on the *Connections* view, or use the quick menu. It refreshes every 30 s; change this with `vanthrex.dashboard.refreshSeconds`.

## Active jobs

**What it is:** A list of your jobs, a user's jobs, a subsystem's jobs, or all active jobs. Jobs in **MSGW** (waiting for a reply) are listed first.

**How:**

- The **filter icon** chooses which jobs to show.
- Click a job to see its **job log**.
- Right-click a job → **Hold**, **Release** or **End Job** (controlled or immediate, with confirmation).

## Messages

**What it is:** The QSYSOPR queue and your own message queue. Messages that are waiting for an answer have a **?** icon.

**How:**

- Click the reply icon, then pick or type a reply (C, D, I, R, G…).
- Hover a message for its full help text.
- Use **Send Message** to message a user or the system operator.

## CL runner and spooled files

- **Ctrl+Alt+L** runs any CL command with your library list. Recent commands are remembered.
- *My Spooled Files:* open, save or delete your spooled output.
