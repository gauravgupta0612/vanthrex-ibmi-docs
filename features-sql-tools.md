---
layout: default
title: "SQL power tools"
nav_order: 10
parent: "Features"
---

# SQL power tools
{: .no_toc }

Generate SQL (DDL), run whole scripts, explain query performance, SQL history and saved queries.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## SQL power tools

- **Generate SQL (DDL):** right-click a file → **Generate SQL (DDL)**, or run the command and type `LIB/OBJECT`. Works for tables, physical and logical files, views, indexes, procedures and functions. The CREATE statement opens in a new SQL editor. Needs a Mapepire SQL engine.
- **Run SQL Script:** **Ctrl+Shift+Enter** in a SQL editor runs every statement in the file (or the selection) one after another. Each statement shows ✔ or ✖, its time, its rows or row count, or its error. It stops at the first error unless you turn off `vanthrex.sql.scriptStopOnError`. It asks once before running destructive statements.
- **SQL history:** every statement you run is remembered (last 50). **SQL History…** lets you run it again, open it, insert it at the cursor or copy it. Click ☆ to save it.
- **Saved queries:** in a SQL editor, right-click → **Save Query…** and give it a name. **Saved Queries…** lists them for running or inserting; the 🗑 button deletes one.

## Explain SQL (performance)

**What it is:** A *Visual Explain*-style summary of a query. New in 0.6.

| You see | Meaning |
|---|---|
| **Table scans** and why | Every row of a table was read — for example *no index exists* |
| **Indexes used** | The indexes or logical files the optimizer chose |
| **Temporary indexes** | Indexes Db2 had to build while running the query |
| **Sorts** and temporary results | Extra work for ORDER BY / GROUP BY |
| **Advised indexes** | Indexes the optimizer recommends for this query, plus the index advisor history of the tables |
| **Advice** | Plain-language tips |

**How:** Put the cursor in a `SELECT` (or select it) in a SQL editor → **Explain SQL (Performance)** in the editor title or the right-click menu. Vanthrex runs the query (first 100 rows) under a database monitor (`STRDBMON`) in your SQL job and shows the report. Click an advised index to get a `CREATE INDEX` statement to review, rename and run. Only queries can be explained, and it needs a Mapepire SQL engine.
