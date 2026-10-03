---
layout: default
title: "Procedure & copybook tools"
nav_order: 11
parent: "Features"
---

# Procedure & copybook tools
{: .no_toc }

Generate prototypes, extract code into procedures, and find unused /COPY members.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Procedure & copybook tools (RPG)

- **Generate prototype from procedure:** put the cursor inside a free-form procedure → right-click → **Generate Prototype from Procedure**. The DCL-PR (return type and every parameter, with their keywords) is copied to the clipboard, ready to paste into your prototype copybook.
- **Extract to procedure:** select whole lines of free-form calculations → right-click → **Extract to Procedure…** and name it. The lines move into a new procedure at the end of the source and are replaced by a call. Vanthrex refuses when that would change what the code does: lines using local variables of the enclosing procedure, RETURN/LEAVE/ITER, declarations, or a block that is opened but not closed (and the other way round). Programs with procedures need `CTL-OPT DFTACTGRP(*NO)`; you are reminded if it is missing.
- **Check /COPY usage:** right-click in an RPG source → **Check /COPY Usage**. Each copybook is listed with the declarations your source uses from it, so unused copybooks stand out. In fully free sources the ☐ button comments the unused ones out.
