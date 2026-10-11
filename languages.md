---
layout: default
title: "Languages"
nav_order: 8
---

# Languages

Vanthrex for IBM i is available in **English, French (Français), Spanish (Español), German (Deutsch), Italian (Italiano), Portuguese – Brazil (Português), Japanese (日本語) and Simplified Chinese (简体中文)** — since version 0.10.
{: .fs-6 .fw-300 }

## Switch the language

Vanthrex uses the VS Code display language:

1. Press **Ctrl+Shift+P** (Cmd+Shift+P on a Mac) and run **Configure Display Language**.
2. Pick the language. If VS Code asks, install its language pack.
3. Restart VS Code.

Commands, menus, views, settings, the Getting Started walkthrough, messages, prompts and report titles then appear in that language.

## What is not translated

- IBM i names: CL commands (CHGDTAARA, GRTOBJAUT…), object types (*FILE, *PGM…), message IDs and SQL.
- IBM's own texts — message help, job logs, object descriptions — come from the IBM i, in the language installed there.
- This documentation site (English only for now).

## Improve a translation

Found a better word, or want another language? [Open an issue](https://github.com/gauravgupta0612/silverlake-ibmi/issues/new/choose). The translations are in `l10n/bundle.l10n.<language>.json` and `package.nls.<language>.json` in the source repository.
