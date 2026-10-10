---
layout: default
title: "SQL & table data"
nav_order: 3
parent: "Features"
---

# SQL & table data
{: .no_toc }

Run Db2 for i SQL with autocomplete and edit table data in a safe grid.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## SQL with results grid and autocomplete

**What it is:** Run Db2 for i SQL from any `.sql` file or the **SQL scratchpad**.

**Why it helps:**

- Results appear in a grid you can sort, filter, copy or export to CSV.
- Table and column names are suggested as you type, and hovering a column shows its type and description.

**How:**

- **New SQL Scratchpad**, put the cursor in a statement, then press **Ctrl+Enter**.
- Type `FROM ` to get table suggestions and `alias.` to get columns.
- Type `ibmi-` for ready-made IBM i Services queries (jobs, job log, locks, PTFs, message queues).

## SQL editor from anywhere (new in 0.7.1)

Right-click a library, source file, member or object in *Libraries & Source* → **Run SQL Query…** — or use **Run SQL…** in the call graph, click an object in the graph, or the button on *Object information* and *Who calls each exported procedure?*.

An SQL editor opens, already filled with a query for what you clicked. Choose another from **Ready-made query**:

| You clicked | Ready-made queries |
|---|---|
| A file | First 100 rows, row count, columns, members and size |
| A program or service program | Program information, bound modules and their source, service programs it is bound to; for a service program also its exported procedures and the programs bound to it |
| A data area / data queue | Its value / its information |
| A library | All objects, tables and views, source members, largest objects |
| A source file or member | Member information, members of the file, most recently changed members |
| Any object | Object details, who has it locked |

Edit the query freely, then **▶ Run** (or Ctrl+Enter) — with several statements, the one under the cursor (or the selected text) runs. The data appears underneath: click a column to sort, type in *Filter rows…*, **Copy as CSV**, or **Open in scratchpad** to keep working on the query.

## Table data editor

**What it is:** A spreadsheet-style editor for any physical file or table.

**Why it helps:**

- It is quicker and safer than DFU or UPDDTA.
- Every value is checked against the column's type and length before anything is written.
- You see a summary and confirm before the changes are saved.

**How:**

- Right-click a file object → **Edit Table Data**, or run the command and type `LIB/FILE`.
- Type a WHERE condition to filter, and use ◀ ▶ to page.
- Click a cell to edit it. Use **+ Row**, **Delete row** and **Set NULL** as needed, then **Save**.
