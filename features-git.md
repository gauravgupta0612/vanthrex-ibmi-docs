---
layout: default
title: "Git for IBM i source"
nav_order: 13
parent: "Features"
---

# Git for IBM i source
{: .no_toc }

Put your RPG, CL and DDS in Git, move changes both ways, and see every version of a member. New in 0.6.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## What it is

Vanthrex keeps a Git repository (on your PC, published to GitHub, GitLab, Azure DevOps, Bitbucket or your own server) in step with source members on the IBM i:

- **Export** a library — or just some source files — into a repository.
- **Get changes from IBM i**: only the members changed on the system since the last sync come in.
- **Upload changed files to IBM i**: only the files you changed go back — to the libraries they came from, or to another library such as your development library.
- **Commit & push** from VS Code.
- **History of a member**: every committed version, with compare and restore.

## Why it helps

- Real version history, branches, pull requests and code review for IBM i source.
- No change to how the IBM i is organised: members stay where they are; Git is an extra copy you control.
- Nothing is overwritten silently: a file changed both in the repository and on the IBM i since the last sync is flagged, and you decide.

## How to use it

### 1. Export a library

Right-click a library (or a source file) in the *Libraries & Source* view → **Git: Export Source to a Git Repository…**

- Pick the source files and the folder.
- Members are saved as `library/sourcefile/member.type`, for example `applib/qrpglesrc/ordentry.rpgle` — VS Code then highlights them as RPG, CL or DDS.
- Vanthrex offers **Create Git Repository & Commit**, then **Publish to GitHub…** (or any remote URL).

Git must be installed on your PC (<https://git-scm.com>).

### 2. Keep both sides in step

| Command | What it does |
|---|---|
| **Git: Get Changes from IBM i** | Downloads members changed on the IBM i since the last sync (and new members). Files you also changed locally are listed separately — tick the ones to overwrite. |
| **Git: Upload Changed Files to IBM i** | Lists files changed in the repository since the last sync (and new files). Untick what you don't want, then choose *into the libraries they came from* or *into another library*. New files become new members (the source file is created if needed). |
| **Git: Commit & Push IBM i Source…** | Commits every change with a message and pushes (or publishes the repository the first time). |

All three are in the quick menu (**Ctrl+Alt+I**) and the Command Palette.

### 3. See every version of a member

In a member editor, open the `…` menu of the editor title (or right-click the member in the tree) → **Git: History of This Member**. Pick a commit, then:

- **Compare this version with the member on IBM i**
- **Compare with the previous version**
- **Open this version** (read-only)
- **Restore this version into the member editor** — then save with **Ctrl+S** to write it to the IBM i.

## Commit author

Commits use your Git configuration (`git config user.name` / `user.email`). To make Vanthrex's commits use a specific name — for example your full name on a shared PC — set:

```json
"vanthrex.git.authorName": "Your Name",
"vanthrex.git.authorEmail": "you@example.com"
```

## Good to know

- `.vanthrex/sync.json` records what was last exchanged (member change time and a hash of the text). Commit it with the source so everyone shares the same baseline.
- Line endings are stored as LF (`.gitattributes` is created for you) and trailing blanks are removed, exactly as members store them.
- With several systems connected, upload asks for confirmation when the active system is not the one the repository was exported from.
