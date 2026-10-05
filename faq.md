---
layout: default
title: FAQ
nav_order: 9
---

# Frequently asked questions
{: .no_toc }

1. TOC
{:toc}

### Is Vanthrex free?

Yes. It is free and open source under the MIT License.

### Is it made by IBM?

No. Vanthrex for IBM i is an independent project by Gaurav Gupta. IBM i is a trademark of IBM Corp.

### How is it different from Code for IBM i?

Both bring IBM i development to VS Code. Vanthrex focuses on an all-in-one, guided experience: SEU-style source dates kept on save, F4 prompters for fixed-format RPG, DDS and CL, a lock banner showing who has a member, conflict protection, a table data editor, a system dashboard, jobs and messages views, and built-in RPG checks — with nothing to install on the server beyond SSH and Java.

### Can I use it alongside Code for IBM i?

Yes. They are separate extensions with their own views and settings. Key bindings can overlap (for example **Ctrl+Alt+C**); change one in **Keyboard Shortcuts** if needed.

### Do I need to install anything on the IBM i?

Only the SSH server must be running. For SQL, Java (5770-JV1) is enough — Vanthrex uploads and starts Mapepire itself. See [IBM i setup](ibm-i-setup.md).

### Where is my password stored?

In the VS Code secret store, which uses the operating system's credential manager. It is never written to settings files. Removing a connection removes its password.

### Will saving a member lose the SEU dates?

No — with a Mapepire SQL engine, untouched lines keep their dates and changed lines get today's date, just like SEU. With db2util, dates are reset.

### Can two people edit the same member?

Vanthrex shows who has the member locked and warns before you overwrite a change someone saved after you opened it. It does not merge automatically; use **Compare First**.

### Does it support IFS source (git-based development)?

Yes. Browse, edit and compile IFS stream files; the compile actions include IFS versions of CRTBNDRPG, CRTSQLRPGI, CRTBNDCL and RUNSQLSTM.

### Can I connect to several systems at once?

You can save many connections, but one is active at a time. Click another connection to switch.

### Does it work on macOS and Linux?

Yes — anywhere VS Code 1.85 or later runs. Use **Cmd** instead of **Ctrl** on a Mac.

### How do I report a bug or ask for a feature?

[Open an issue](https://github.com/gauravgupta0612/silverlake-ibmi/issues/new/choose) or use **Q & A** on the [Marketplace page](https://marketplace.visualstudio.com/items?itemName=gauravgupta0612.vanthrex-ibmi).

### Which AI model does `@vanthrex` use? Where does my code go?

The model you select in the VS Code chat (for example a GitHub Copilot model). Vanthrex sends the code you ask about, the system name, release and library list, and the results of the look-ups it makes to that model — nothing else. Turn the assistant off with `vanthrex.ai.enabled`, or stop the look-ups with `vanthrex.ai.useTools`. Check your company's rules before sending confidential source to an AI service.

### Can the AI change data or run commands on my IBM i?

No. It only has read tools: describe objects, read source, search objects, system status and read-only queries (single SELECT / WITH / VALUES, with known side-effect functions refused). Vanthrex asks before each query and before reading an IFS file.

### Do I need GitHub to use the Git features?

No. Any Git remote works (GitLab, Azure DevOps, Bitbucket, your own server) — or no remote at all, just a local repository for history.

### Can I be connected to DEV and PROD at the same time?

Yes, since 0.6. Switch with **Switch IBM i System**; files are always saved to the system they came from.

