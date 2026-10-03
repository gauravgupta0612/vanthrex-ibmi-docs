---
layout: default
title: "SEU-style editing"
nav_order: 4
parent: "Features"
---

# SEU-style editing
{: .no_toc }

Source dates, F4 prompters and member lists with dates — what SEU users expect, in VS Code.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## SEU-style source dates

**What it is:** Every line of a member shows when it was last changed, like the date column in SEU. Lines you edit show today's date (highlighted) until you save.

**Why it helps:** You can see at a glance what changed recently, and saving keeps the dates of every line you didn't touch.

**How:**

- **Ctrl+Alt+D** (or the 📅 icon in the editor title) cycles between *date*, *sequence number + date* and *hidden*.
- Hover the start of a line for its sequence number and full date.
- Right-click → **Highlight Lines Changed Since…** (7, 30 or 90 days, or any date) highlights the lines and lists them so you can jump between them.
- Settings: `vanthrex.sourceDates.format` chooses `yymmdd` (SEU) or `iso`.

## F4 prompters

**What it is and how to use it:**

- **Fixed-format RPG and DDS:** put the cursor on a C, D, F, H or P spec (or a DDS line) and press **F4**. A form shows each column area with its name (Factor 1, Opcode, Result field, Length…) and allowed values. **Apply** writes it back in the right columns. **Apply & next line** keeps going, like SEU. On a blank line, F4 asks which spec to create.
- **CL commands:** in a CL source, press **F4** on a command. Vanthrex reads the command's real definition from the IBM i and shows every parameter with its prompt text, default and allowed values. The command is rewritten in proper CL source layout, with `+` continuations.
- **Prompt and Run CL Command** (quick menu): type a command name, fill in the form, and it runs.

## Member list with dates

- Each member shows its **last change date** in the tree. The tooltip adds the creation date and line count.
- **Sort Members by Name / Date** (Libraries view toolbar) puts the most recently changed members first.
- Right-click a source file → **Filter Members by Last Change…** shows only members changed today, or in the last 7, 30 or 90 days, or any number of days.
