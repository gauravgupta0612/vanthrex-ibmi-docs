---
layout: default
title: "Locks & conflicts"
nav_order: 5
parent: "Features"
---

# Locks & conflicts
{: .no_toc }

See who has a member, ask them to release it, and never overwrite someone else's change.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Who has my member? (locks)

**What it is:** When a member is open somewhere else (for example in SEU), the editor shows a banner at the top: **🔒 Locked by *name* (USER) · job … · *SHRUPD**.

**How:**

- **✉ Ask to release** sends a message that pops up on their screen (break message), or goes to their message queue.
- **🔔 Notify me when free** checks every 15 seconds and tells you when the lock is gone.
- **More options:** show their job log, or end their job (needs *JOBCTL authority, and they lose unsaved work, so you are asked to confirm).

## Edit conflict protection

**What it is:** Before saving, Vanthrex checks whether the member changed on the IBM i after you opened it, or is locked by another job.

**How:** You get **Compare First** (opens a side-by-side diff with the IBM i copy) or **Overwrite**. Turn it off with `vanthrex.conflictCheck`.
