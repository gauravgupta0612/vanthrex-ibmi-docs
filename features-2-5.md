---
layout: default
title: "New in 2.5"
nav_order: 28
parent: "Features"
---

# New in 2.5: AI with your data protected
{: .no_toc }

More AI help for IBM i developers and operators, and one guard in front of every request so that secrets, personal data and production data stay on your side.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## What the AI never sees

| Protection | How | Setting |
|---|---|---|
| Secrets | Passwords (CL `PASSWORD(…)`, `pwd = …`, constants named like a password), API keys, tokens, JWTs, private keys, credentials in URLs are replaced by placeholders (xxxx1…) before sending. The real values are put back only on your computer. | `vanthrex.ai.redact.secrets` |
| Personal data | E-mail addresses, payment card numbers (Luhn-checked), IBANs (checksum-checked). | `vanthrex.ai.redact.personalData` |
| Internal names | IP addresses, the host names of your connections, your own list. | `vanthrex.ai.redact.hostNames`, `…hostList` |
| Your words | Customer names, project code names. | `vanthrex.ai.redact.words` |
| Sensitive columns | Query results show `xxxx` for PASSWORD, EMAIL, PHONE, IBAN, CARD, SALARY, BIRTH… | `vanthrex.ai.sensitiveColumns` |
| Production data | On protected connections: source and catalog facts only — no queries of the AI's own, no spooled files, no non-source IFS files. | `vanthrex.ai.productionData`, `vanthrex.ai.otherSystemsData` |
| Risky queries | Queries the AI writes may not call HTTP, IFS-read, spooled-file, journal, data-queue or QCMDEXC functions, nor rename a sensitive column. | — |
| Links | Real values are never put back inside a link or URL of an answer, and only for what that request sent. | — |
| Libraries | Never read (wildcards like `PAY*`). | `vanthrex.ai.deniedLibraries` |
| Key files | IFS files that look like keys, certificates, credentials or system files, /QSYS.LIB paths and members of data files are refused. | — |
| Hidden instructions | System data is framed as data; the model is told never to obey it. | — |
| Changes | Queries are read-only and ask first; code changes are a diff you apply yourself. | `vanthrex.ai.confirmQueries` |

**See it:** after each answer Vanthrex says how many values were hidden. *AI: Privacy and Security* shows the settings, the counts and every request (time, system, feature, size — never the content). *AI: Preview What the AI Sees* compares the open file with what would be sent. The audit trail is also written to the *Vanthrex AI Audit* output and a file (`vanthrex.ai.audit`).

## New AI features

| Feature | How |
|---|---|
| Change the selected code | **Ctrl+Alt+E**: describe the change; the proposal opens as a diff; *Apply* or not. |
| ✨ links above procedures | *Explain · Document · Tests* for one procedure or subroutine (`vanthrex.ai.codeLens`). |
| `/tune` | Faster SQL with table sizes, indexes and index advice; CREATE INDEX proposals. |
| `/sqlio` | Native file I/O to embedded SQL. |
| `/changes` | Review only your changes (Git HEAD, unsaved changes, or the latest source-date day). |
| `/cl` | CL from a description, with the real command definitions. |
| `/data LIB/TABLE` | Invented test data that respects types and keys — structure only. |
| `/health` | What needs attention on the system now. |
| `/security LIB/OBJ` | Authority review with the commands to fix each finding. |
| `/spool` | A spooled file explained (right-click it). |
| Agent-mode tools | `#ibmiMessage`, `#ibmiMembers`, `#ibmiCommand`, `#ibmiIndexes`. |
