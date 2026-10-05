---
layout: home
title: Home
nav_order: 1
description: "Vanthrex for IBM i — connect, browse, edit, compile, query and monitor IBM i from VS Code."
permalink: /
---

# Vanthrex for IBM i
{: .fs-9 }

One sidebar for everything you do on IBM i: connect, browse, edit, compile, query, monitor and fix — with an AI assistant, Git and a call graph built in — without leaving VS Code and without a green screen.
{: .fs-6 .fw-300 }

[Install from the Marketplace](https://marketplace.visualstudio.com/items?itemName=gauravgupta0612.vanthrex-ibmi){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }
[Get started](installation.md){: .btn .fs-5 .mb-4 .mb-md-0 .mr-2 }
[View on GitHub](https://github.com/gauravgupta0612/silverlake-ibmi){: .btn .fs-5 .mb-4 .mb-md-0 }

---

## What you can do

| | |
|---|---|
| **Connect in a minute** | A guided form with **Test connection**. Only SSH is needed on the IBM i — fast SQL is set up automatically. |
| **Edit like SEU, but better** | Members open like local files, show each line's **change date**, keep dates on save, and **F4** prompts RPG specs, DDS and CL commands. |
| **Compile with one key** | **Ctrl+Alt+C** picks the right command and puts compile errors on the exact line. |
| **Query and edit data** | **Ctrl+Enter** runs Db2 for i SQL with autocomplete; edit table rows in a safe, validated grid. |
| **Work as a team** | See **who has a member locked**, ask them to release it, and get warned before overwriting someone else's change. |
| **Keep the system healthy** | Dashboard, active jobs, QSYSOPR replies, spooled files and a CL runner. |
| **Know your objects** | Object information, who has an object locked, and **compare DEV with PROD** — new in 0.4. |
| **SQL power tools** | Generate DDL, run whole scripts, SQL history and saved queries — new in 0.4. |
| **Debug** | Breakpoints, stepping, variables and call stack for RPG, COBOL and CL — **Ctrl+Alt+G**, new in 0.5. |
| **Ask the AI** | **@vanthrex** in the VS Code chat explains, documents, reviews and modernizes RPG, writes SQL against your real tables and fixes compile errors — [new in 0.6](features-ai.md). |
| **Source in Git** | Export libraries to Git, move changes both ways and see every version of a member — [new in 0.6](features-git.md). |
| **See the impact** | Interactive **call graph** of callers and callees before you change a program or file — [new in 0.6](features-call-graph.md). |
| **DEV, TEST and PROD together** | Several systems connected at once, switch instantly; SQL **Explain** shows scans and advised indexes — new in 0.6. |
| **Understand the code** | Object and source search, **where used**, go to definition into /COPY members, scoped rename and RPG code checks. |

## Start here

1. [Install the extension](installation.md)
2. [Check the IBM i requirements](ibm-i-setup.md) (usually just `STRTCPSVR SERVER(*SSHD)`)
3. [Create your first connection](first-connection.md)
4. Browse the [features](features.md) or the [keyboard shortcuts](keyboard-shortcuts.md)

Something not working? See [Troubleshooting](troubleshooting.md).

---

Current version: **0.6.1** · [Changelog](changelog.md) · Free and open source under the MIT License.
