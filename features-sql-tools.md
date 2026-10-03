---
layout: default
title: "SQL power tools"
nav_order: 10
parent: "Features"
---

# SQL power tools
{: .no_toc }

Generate SQL (DDL), run whole scripts, SQL history and saved queries.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## SQL power tools

- **Generate SQL (DDL):** right-click a file → **Generate SQL (DDL)**, or run the command and type `LIB/OBJECT`. Works for tables, physical and logical files, views, indexes, procedures and functions. The CREATE statement opens in a new SQL editor. Needs a Mapepire SQL engine.
- **Run SQL Script:** **Ctrl+Shift+Enter** in a SQL editor runs every statement in the file (or the selection) one after another. Each statement shows ✔ or ✖, its time, its rows or row count, or its error. It stops at the first error unless you turn off `vanthrex.sql.scriptStopOnError`. It asks once before running destructive statements.
- **SQL history:** every statement you run is remembered (last 50). **SQL History…** lets you run it again, open it, insert it at the cursor or copy it. Click ☆ to save it.
- **Saved queries:** in a SQL editor, right-click → **Save Query…** and give it a name. **Saved Queries…** lists them for running or inserting; the 🗑 button deletes one.
