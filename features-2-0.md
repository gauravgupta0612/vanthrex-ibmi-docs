---
layout: default
title: "New in 2.0"
nav_order: 22
parent: "Features"
---

# New in 2.0
{: .no_toc }

Twenty helpers for development, data and operations.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Development helpers

- **Generate RPG Code for This Table** (right-click a file): a qualified template data structure and get / add / update / delete / list procedures in embedded SQL, opened as a new RPG document. When the table has no primary key, you pick the key columns.
- **Format SQL**: Shift+Alt+F (or right-click → Format SQL) in a `.sql` editor; also formats a selection.
- **Find and Replace in Source File…** (right-click a source file): text, whole word, match case or regular expression, previewed line by line; **Apply** keeps source dates (changed lines get today's date), skips members in use, and never makes a line longer than the source file allows.
- **Compile Changed Members…** (right-click a source file): members changed today / 7 / 30 days, or picked by hand, compiled with the matching compile action; the result page lists failures first.
- **Print Preview (Printer File)** in a PRTF member: the record formats printed once each on a page, with a ruler.
- **Copy Members to Another Source File…**, **Copy Objects to Another Library…**, **Rename or Move…** on the Libraries view.
- **Find a CL Command…**: search by keyword, then prompt the command with F4.

## Data tools

- **Export Table Data** now also writes **SQL INSERT statements**.
- **Generate Test Data…** (right-click a file): pick a row count, preview, then insert. Numeric keys continue after the highest existing value.
- **Find Duplicate Rows…** (right-click a file): pick the columns that should be unique.
- **Table Statistics** (right-click a library): rows, deleted rows, size, last change and use of every table.

## Operations helpers

- **Submit to Batch and Watch…** (quick menu) and **Watch This Job** (Jobs view): a spinner in the status bar while the job runs, a notification when it ends with its end code, and Job Log / Analyze buttons.
- **My Recent Jobs** (Jobs view toolbar): your recent jobs with completion status.
- **Compare with Another Spooled File…** (Spooled Files view): side-by-side diff of two spooled files.
- **Follow File (tail -f)** on an IFS file (`vanthrex.ifs.followLines`), and **Search Text in Files…** on an IFS folder.
- **Library List Sets…** (quick menu or right-click the active connection): save, switch and delete named library lists per system.

