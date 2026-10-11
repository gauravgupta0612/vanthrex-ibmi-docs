---
layout: default
title: "Insights"
nav_order: 15
parent: "Features"
---

# Insights
{: .no_toc }

Index advisor, table data compare, message help and the job log analyzer — new in 0.8.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Index advisor

**What it is:** All the indexes Db2 for i recommended while your programs and queries ran (`QSYS2.SYSIXADV`), for your library list, one library or all user libraries: table, key columns, how often and when it was advised, and how expensive the slowest query was.

**Why it helps:** A missing index is the most common reason for a slow program. *Explain SQL* shows the advice for one statement; the advisor shows everything Db2 has learned, ranked, so you fix the biggest wins first.

**How:** Right-click a library → **Index Advisor** (or the quick menu). Click a suggestion → confirm the proposed name → **Create Index** (or **Copy SQL**). **Show Queries Running Now** lists the active SQL statements.

## Compare table data (DEV ↔ PROD)

**What it is:** Compares the rows of the same table in two libraries, matched by key columns.

**Why it helps:** "It works in test but not in production" is often a data difference. You see exactly which rows are only on one side and which fields changed.

**How:** Right-click a file → **Compare Table Data**, pick the other library and the key columns (the primary key is pre-selected). The page shows exact counts, the changed rows field by field, and the rows only in one copy. **Export differences (CSV)** saves them. Needs a Mapepire SQL engine.

## Message help and job log analyzer

- **Hover any message ID** — CPF, CPD, MCH, RNQ/RNX, SQL, CEE… — in any editor (job logs, compile listings, spooled files, comments) to see IBM's message text, severity, a plain-language *what to do*, and the full help text.
- **Explain Message ID…** (quick menu) shows the same for an ID you type.
- **Analyze Job Log**: right-click a job in *Active Jobs* (or run the command and type a job name). Errors are grouped, the most likely root cause is highlighted — the first real escape message, not the generic CPF9999 function check — with advice, and each message opens its full explanation.
