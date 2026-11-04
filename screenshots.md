---
layout: default
title: "Screenshots"
nav_order: 3
description: "Screenshots of Vanthrex for IBM i in VS Code."
---

# Screenshots
{: .no_toc }

What Vanthrex looks like in VS Code. Click a picture to open it full size.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## Write better code

### Checks while you type

More than 50 checks for RPG, CL and SQL as you type, in the *Problems* view. [Read more](features-rpg-checks.md)

[![Checks while you type]({{ "/images/rpg-checks.png" | relative_url }})]({{ "/images/rpg-checks.png" | relative_url }})

### Quick fixes

`Ctrl+.` on a warning adds the missing code — here an `IF NOT %FOUND` test after `CHAIN`. [Read more](features-rpg-checks.md)

[![Quick fixes]({{ "/images/quick-fix.png" | relative_url }})]({{ "/images/quick-fix.png" | relative_url }})

### Suggestions while you type

The next line an IBM i developer would write appears in grey; `Tab` accepts it. [Read more](features-2-6.md#suggestions-while-you-type)

[![Suggestions while you type]({{ "/images/suggestions.png" | relative_url }})]({{ "/images/suggestions.png" | relative_url }})

### CL checks

Undeclared variables, missing labels, values too long and hard-coded libraries in CL. [Read more](features-2-6.md#cl-checks-while-you-type)

[![CL checks]({{ "/images/cl-checks.png" | relative_url }})]({{ "/images/cl-checks.png" | relative_url }})

### SQL checks

`DELETE` / `UPDATE` without `WHERE`, `= NULL` and statements that cannot be undone. [Read more](features-2-6.md#sql-checks)

[![SQL checks]({{ "/images/sql-checks.png" | relative_url }})]({{ "/images/sql-checks.png" | relative_url }})

### DDS checks

Names, decimals, lengths, fields outside the screen and overlapping fields in PF, LF, DSPF and PRTF sources. [Read more](features-3-1.md)

[![DDS checks]({{ "/images/dds-checks.png" | relative_url }})]({{ "/images/dds-checks.png" | relative_url }})

### Team coding standards

Tick the rules your team follows (or import your rpglint.json); they are checked while you type. [Read more](features-3-0.md)

[![Team coding standards]({{ "/images/team-standards.png" | relative_url }})]({{ "/images/team-standards.png" | relative_url }})

## Modernize and understand

### Fixed → free

One command converts H, F, D, P and C specs to free format. [Read more](features-edit-compile.md#fixed--free-format-conversion)

[![Fixed → free]({{ "/images/fixed-to-free-compare.png" | relative_url }})]({{ "/images/fixed-to-free-compare.png" | relative_url }})

### Flowchart of a procedure

Click a box to go to its line; copy the chart as Mermaid. [Read more](features-2-5.md#modernize-and-understand-code)

[![Flowchart of a procedure]({{ "/images/flowchart.png" | relative_url }})]({{ "/images/flowchart.png" | relative_url }})

### Data structure layout

Every subfield with its positions and length, like the compile listing — without compiling. [Read more](features-2-3.md#data-structure-layout)

[![Data structure layout]({{ "/images/ds-layout.png" | relative_url }})]({{ "/images/ds-layout.png" | relative_url }})

### Code metrics

Lines, procedures, complexity and nesting, with a grade. [Read more](features-data-quality.md#code-metrics-and-documentation)

[![Code metrics]({{ "/images/code-metrics.png" | relative_url }})]({{ "/images/code-metrics.png" | relative_url }})

### Format Document for CL

`Shift+Alt+F` puts CL in the prompter layout and splits long commands. [Read more](features-3-1.md)

[![Format Document for CL]({{ "/images/cl-format-compare.png" | relative_url }})]({{ "/images/cl-format-compare.png" | relative_url }})

## Work faster

### Developer Toolbox

`Ctrl+Alt+A`: every tool that fits the file you are in. [Read more](features-2-6.md#developer-toolbox)

[![Developer Toolbox]({{ "/images/developer-toolbox.png" | relative_url }})]({{ "/images/developer-toolbox.png" | relative_url }})

### The Vanthrex side bar

Everything starts from the Vanthrex icon in the activity bar. [Read more](first-connection.md)

[![The Vanthrex side bar]({{ "/images/sidebar.png" | relative_url }})]({{ "/images/sidebar.png" | relative_url }})

### Connect in a minute

A guided form with **Test connection**; only SSH is needed on the IBM i. [Read more](first-connection.md)

[![Connect in a minute]({{ "/images/add-connection.png" | relative_url }})]({{ "/images/add-connection.png" | relative_url }})
