---
layout: default
title: Installation
parent: Getting started
nav_order: 1
---

# Installation
{: .no_toc }

1. TOC
{:toc}

## From the VS Code Marketplace (recommended)

1. In VS Code, open the **Extensions** view (**Ctrl+Shift+X**).
2. Search for **Vanthrex for IBM i**.
3. Click **Install**.

Or open the [Marketplace page](https://marketplace.visualstudio.com/items?itemName=gauravgupta0612.vanthrex-ibmi) and click **Install**, or run this in a terminal:

```bash
code --install-extension gauravgupta0612.vanthrex-ibmi
```

A **Vanthrex** icon appears in the activity bar on the left. VS Code updates the extension automatically when a new version is published.

## Offline (VSIX file)

Use this when your PC can't reach the Marketplace.

1. Download `vanthrex-ibmi-<version>.vsix` from the [GitHub Releases page](https://github.com/gauravgupta0612/silverlake-ibmi/releases).
2. In VS Code: **Extensions** view → `…` menu → **Install from VSIX…** → choose the file.

## Requirements on your PC

- VS Code **1.85** or later (Windows, macOS or Linux).
- Network access to the IBM i's SSH port (22 by default).

## Build from source

```bash
git clone https://github.com/gauravgupta0612/silverlake-ibmi.git
cd silverlake-ibmi
npm install
npm test            # unit tests for the parsers and the RPG converter
npm run package     # creates vanthrex-ibmi-<version>.vsix
```

Press **F5** in VS Code to start an Extension Development Host with the extension loaded.

## Upgrading from Silverlake

Vanthrex was called *Silverlake* before 0.3.0. Settings now start with `vanthrex.` instead of `silverlake.`, so add your connections again after installing and uninstall the old extension.

**Next:** [IBM i setup](ibm-i-setup.md)
