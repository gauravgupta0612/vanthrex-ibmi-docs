---
layout: default
title: Debugging
nav_order: 5
---

# Debugging RPG, COBOL and CL
{: .no_toc }

Breakpoints, stepping, variables and the call stack — in VS Code's normal debug view.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## How it works

Vanthrex starts your program in a **batch job** under the IBM i debugger and opens a VS Code debug session for it. Two IBM components do the debugging itself:

| Component | Where | What it is |
|---|---|---|
| **IBM i Debug** extension | VS Code on your PC | IBM's free debug client ([Marketplace](https://marketplace.visualstudio.com/items?itemName=IBM.ibmidebug)). Vanthrex installs it for you on request. |
| **IBM i Debug Service** | The IBM i | IBM's debug server, delivered by PTF. It listens on a secured port (usually **8005**) and needs a certificate. |

Vanthrex reads the Debug Service configuration (`/QIBM/ProdData/IBMiDebugService/bin/DebugService.env`), finds its port and certificate, downloads the certificate so your PC trusts the server, and starts the session.

## Debug a program

1. Compile the program with `DBGVIEW(*SOURCE)` — every built-in compile action does.
2. Open the source and click in the gutter to set breakpoints.
3. Press **Ctrl+Alt+G** (or the 🐞 button in the editor title, or right-click the program in *Libraries & Source → Objects* → **Debug Program**).
4. Confirm the program (`LIBRARY/PROGRAM`) and the command that starts it. Add `PARM(...)` when it needs parameters, for example `CALL PGM(MYLIB/ORDENTRY) PARM('A' 42)`. Vanthrex remembers the command per program.
5. The program runs in a batch job with your connection's library list and current library; execution stops at your breakpoints. Use the debug toolbar to continue, step over, step into and step out, and the *Variables*, *Watch* and *Call Stack* views.

{: .note }
Production libraries are protected: the debugged program can't update files in them unless you turn on `vanthrex.debug.updateProductionFiles`.

## First-time setup check

Run **Vanthrex: Debugger Setup Check** (quick menu **Ctrl+Alt+I** → *Debugger setup check*, or the `…` menu of the *Connections* view). It checks:

| Check | How to fix it |
|---|---|
| IBM i Debug extension installed | Click **Install IBM i Debug extension**. |
| Debug Service installed on the IBM i | Ask your administrator to install the PTFs (below). |
| Debug Service running | Click **Start Debug Service** (Vanthrex submits IBM's start script as job QDBGSRV), or start it in IBM i Navigator → Network → Servers → TCP/IP Servers → **Debug Service**. |
| Server certificate generated | One-time administrator task (below). |
| Certificate trusted on this PC | Click **Download certificate**. |

## Administrator setup (once per system)

1. **Install the PTFs** for the Debug Service on your release. IBM lists them on its [Debug Service support page](https://www.ibm.com/support/pages/debug-service) (7.3 SI80858, 7.4 SI81031, 7.5 SI81035), and the [IBM i Debug extension page](https://marketplace.visualstudio.com/items?itemName=IBM.ibmidebug) lists the current levels it needs (7.3 SJ08544, 7.4 SJ08540, 7.5 SJ08535, 7.6 SJ08472).
2. **Create the certificate**: a keystore (`debug_service.pfx`) with a self-signed certificate, by IBM i Navigator's Debug Service configuration or with `keytool` / `openssl`, as described in [Configuring TLS on the IBM i Debugger server](https://www.ibm.com/docs/en/i/7.6.0?topic=tls-configuring-i-debugger-server). Put the matching public certificate (`debug_service.crt`) next to it (by default in `/QIBM/UserData/IBMiDebugService/certs/`) so clients can download it.
3. **Authorities** (from IBM's documentation): `QDBGSRV` starts the service and needs `CHGAUT OBJ('/QIBM/UserData/IBMiDebugService/startDebugService_workspace') USER(QDBGSRV) DTAAUT(*RWX)`; `QSECOFR` (or `QSECOFR_NC` on 7.6) must be enabled.
4. Start the Debug Service and run Vanthrex's setup check from a PC.

## Settings

| Setting | Default | Purpose |
|---|---|---|
| `vanthrex.debug.port` | 0 | Secured port of the Debug Service. 0 = read it from the service configuration (usually 8005). |
| `vanthrex.debug.ignoreCertificateErrors` | false | Connect even when the certificate can't be verified — test systems only. |
| `vanthrex.debug.updateProductionFiles` | false | Let the debugged program update files in production libraries. |
| `vanthrex.debug.trace` | false | Trace the debug protocol (for support). |

## Troubleshooting

- **"The debug session did not start"** — run the setup check; most often the service isn't running or the certificate isn't trusted. Open **View → Output → IBM i Debug** for the client's messages.
- **Breakpoints are hollow / never hit** — compile with `DBGVIEW(*SOURCE)` and debug the program you just compiled (check the library).
- **The program needs a display** — batch debugging can't show 5250 screens; debug the business logic in a program called without a display.
- **Your password** — the Debug Service signs in with your IBM i password. With key sign-in, Vanthrex asks for it each time.

## Limitations

- Programs are debugged in a **batch job**. Service entry points (debugging a program when another job calls it) are on the [roadmap](roadmap.md).
- Interactive programs that use display files can't be debugged in batch.
