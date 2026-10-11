---
layout: default
title: "Call graph & impact analysis"
nav_order: 14
parent: "Features"
---

# Call graph & impact analysis
{: .no_toc }

See who calls a program or uses a file — and what it uses — as an interactive diagram. New in 0.6.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## What it is

An interactive diagram built from the program cross-reference (DSPPGMREF) of the libraries you choose:

- **Callers (impact):** programs that call the object or use the file, then the programs that call those, and so on.
- **Callees:** programs, service programs, files and data areas the object uses, several levels deep. File links show the usage: *input*, *output*, *update*.

## Why it helps

Before changing a file layout, a program's parameters or a service program export, you see every program affected — across libraries — in seconds, instead of running DSPPGMREF by hand and reading printouts.

## How to use it

1. Right-click a program, service program or file in the *Libraries & Source* view → **Call Graph…** or **Impact Analysis (Who Uses This?)…** (or quick menu → *Call graph & impact analysis*, then type `LIB/NAME *TYPE`).
2. Choose which libraries hold the programs to analyse: your library list, one library, or a list.
3. Work with the graph:
   - **◀ Callers / Both / Callees ▶** — which direction to show.
   - **− / +** — fewer or more levels (start level: `vanthrex.callGraph.depth`).
   - **Hide files**, **Fit**, drag to pan, scroll to zoom.
   - Click an object → centre the graph on it, object information, open source, edit data, or **ask the AI** about it.
   - **Copy as Mermaid** — paste the diagram into a README, wiki or pull request.
   - **Rebuild cross-reference** after you compile or add programs.

The header shows the impact: how many programs in which libraries use the object.

## Good to know

- Needs a Mapepire SQL engine (the cross-reference is built in QTEMP).
- IBM-supplied objects (QCMDEXC, QSYSPRT…) are hidden; show them with `vanthrex.callGraph.hideSystemObjects`.
- Objects referenced through `*LIBL` are matched to the analysed libraries; if they are elsewhere they show as `*LIBL/NAME`.
- Dynamic calls (a program name in a variable) can't be seen by DSPPGMREF.
- Large graphs are cut at `vanthrex.callGraph.maxNodes` objects (default 200).
