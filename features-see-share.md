---
layout: default
title: "See and share"
nav_order: 21
parent: "Features"
---

# See and share
{: .no_toc }

5250 screen preview, database diagrams, comparing two systems, and spooled files to PDF and e-mail — new in 1.3.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Screen preview for display files

**What it is:** A 5250-style drawing of a DSPF record format: constants, input fields (underlined), output fields (X / 9), COLOR and DSPATR, 24×80 or 27×132, WINDOW records, and a subfile control drawn with SFLPAG rows of its subfile, plus a table of the record's fields.

**How:** In a DSPF member, **Preview Screen** in the editor title (or right-click). It shows the record your cursor is in and updates as you type; pick another record from the list; click a field to go to its source line. Every conditioned field is shown, as if all indicators were on.

## Database diagram

**What it is:** An entity-relationship diagram of a library: tables and physical files with their columns and primary keys, declared foreign keys, and relationships inferred from column names that match another table's one-column primary key (dashed).

**How:** Right-click a library → **Database Diagram** (pick the tables when there are more than 40). Click a table to highlight its links, Ctrl+wheel or +/− to zoom, **Copy as Mermaid** or **Save as SVG**.

## Compare with another system

**What it is:** Compare DEV and PROD (or any two connected systems): a source member side by side, the objects of a library (attribute and source date, newer side), the rows of a table by key, the system values, or the PTF group levels.

**How:** Connect to both systems, then quick menu → **Compare with another system…**. Table compares read at most `vanthrex.compare.maxRows` rows per system.

## Spooled files to PDF and e-mail

- **Save as PDF…** on a spooled file: paged like the original; made locally from the text, or by the IBM i (`vanthrex.spool.pdfMode: server`, CPYSPLF WSCST(*PDF)) to keep fonts and graphics.
- **Send by E-mail…** on a spooled file attaches the PDF; **E-mail Query Result** in a `.sql` editor attaches the result as Excel. Mail is sent by the IBM i with SNDSMTPEMM, so SMTP must be set up there.

