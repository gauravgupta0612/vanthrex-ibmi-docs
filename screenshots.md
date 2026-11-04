---
layout: default
title: Screenshots
nav_order: 2.5
description: "Screenshots of Vanthrex for IBM i in VS Code."
---

# Screenshots
{: .no_toc }

What Vanthrex looks like in VS Code. Click a picture to see it full size.

1. TOC
{:toc}

## Checks while you type

More than 50 checks for RPG, CL and SQL run as you type — prototypes that no longer match, wrong argument counts, array indexes out of range, numeric overflow, CHAIN without %FOUND — and land in the *Problems* view. [Read more](features-rpg-checks.html)

[![Checks while you type]({{ "/images/rpg-checks.png" | relative_url }})]({{ "/images/rpg-checks.png" | relative_url }})

## Quick fixes

Press `Ctrl+.` on a warning: Vanthrex adds the missing code (here an `IF NOT %FOUND` test after `CHAIN`) or lets you turn the check off. [Read more](features-rpg-checks.html)

[![Quick fixes]({{ "/images/quick-fix.png" | relative_url }})]({{ "/images/quick-fix.png" | relative_url }})

## Suggestions while you type

The next line an IBM i developer would write appears in grey — `IF %FOUND` after `CHAIN`, an SQLCODE test after embedded SQL, `MONMSG` after `CHKOBJ`. Press `Tab` to accept. [Read more](features-2-6.html)

[![Suggestions while you type]({{ "/images/suggestions.png" | relative_url }})]({{ "/images/suggestions.png" | relative_url }})

## Developer Toolbox

`Ctrl+Alt+A` opens one menu with every tool that fits the file you are in. [Read more](features-2-6.html)

[![Developer Toolbox]({{ "/images/developer-toolbox.png" | relative_url }})]({{ "/images/developer-toolbox.png" | relative_url }})

## CL checks

Undeclared variables, labels that do not exist, values too long for a variable and hard-coded libraries in CL sources — with a quick fix to declare the variable. [Read more](features-2-6.html)

[![CL checks]({{ "/images/cl-checks.png" | relative_url }})]({{ "/images/cl-checks.png" | relative_url }})

## SQL checks

`UPDATE` / `DELETE` without `WHERE`, `= NULL` that is never true and statements that cannot be undone — found in SQL scripts before you run them. [Read more](features-2-6.html)

[![SQL checks]({{ "/images/sql-checks.png" | relative_url }})]({{ "/images/sql-checks.png" | relative_url }})

## Connect in a minute

A guided form with **Test connection**. Only SSH is needed on the IBM i. [Read more](first-connection.html)

[![Connect in a minute]({{ "/images/add-connection.png" | relative_url }})]({{ "/images/add-connection.png" | relative_url }})

## Team coding standards

Tick the standards your team follows (or import your rpglint.json): they are checked while you type, and the code health report checks whole libraries. [Read more](features-3-0.html)

[![Team coding standards]({{ "/images/team-standards.png" | relative_url }})]({{ "/images/team-standards.png" | relative_url }})
