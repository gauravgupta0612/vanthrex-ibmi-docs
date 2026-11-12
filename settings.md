---
layout: default
title: "Settings"
parent: Reference
nav_order: 2
---

# Settings

Open **File → Preferences → Settings** and search for *Vanthrex*, or edit `settings.json`.

<table class="settings-table">
<thead><tr><th>Setting</th><th>Type</th><th>Default</th><th>Description</th></tr></thead>
<tbody>
<tr><td><code>vanthrex.compileActions</code></td><td>array</td><td>15 built-in actions</td><td>Compile actions. Variables: <code>&amp;LIB</code> (source library), <code>&amp;OBJLIB</code> (target library), <code>&amp;SRCFILE</code>, <code>&amp;NAME</code>, <code>&amp;EXT</code>, <code>&amp;FULLPATH</code> (IFS path), <code>&amp;CURLIB</code>, <code>&amp;USER</code>. Add <code>OPTION(*EVENTF)</code> to get inline errors.</td></tr>
<tr><td><code>vanthrex.sql.maxRows</code></td><td>number</td><td><code>500</code></td><td>Maximum number of rows fetched into the SQL result grid.</td></tr>
<tr><td><code>vanthrex.sql.confirmDestructive</code></td><td>boolean</td><td><code>true</code></td><td>Ask for confirmation before running DELETE, DROP, TRUNCATE or UPDATE without WHERE.</td></tr>
<tr><td><code>vanthrex.tempDirectory</code></td><td>string</td><td><code>"/tmp"</code></td><td>IFS directory used for temporary files during member transfer.</td></tr>
<tr><td><code>vanthrex.spool.maxEntries</code></td><td>number</td><td><code>200</code></td><td>Maximum number of spooled files listed.</td></tr>
<tr><td><code>vanthrex.autoConnectLast</code></td><td>boolean</td><td><code>false</code></td><td>Reconnect automatically to the last used system when VS Code starts.</td></tr>
<tr><td><code>vanthrex.objects.showAll</code></td><td>boolean</td><td><code>true</code></td><td>Show an 'Objects' folder (programs, files, service programs…) under each library.</td></tr>
<tr><td><code>vanthrex.dashboard.refreshSeconds</code></td><td>number</td><td><code>30</code></td><td>How often the System Dashboard refreshes (seconds). 0 = only when you click Refresh.</td></tr>
<tr><td><code>vanthrex.dataEditor.pageSize</code></td><td>number</td><td><code>100</code></td><td>Rows per page in the table data editor.</td></tr>
<tr><td><code>vanthrex.history.enabled</code></td><td>boolean</td><td><code>true</code></td><td>Keep a local copy of every member and IFS file you open or save, so you can compare and restore.</td></tr>
<tr><td><code>vanthrex.history.maxVersions</code></td><td>number</td><td><code>50</code></td><td>Local history versions kept per member / file.</td></tr>
<tr><td><code>vanthrex.lint.enabled</code></td><td>boolean</td><td><code>true</code></td><td>Check RPG sources as you type.</td></tr>
<tr><td><code>vanthrex.lint.maxProcedureLines</code></td><td>number</td><td><code>200</code></td><td>Report procedures longer than this many lines.</td></tr>
<tr><td><code>vanthrex.lint.rules</code></td><td>object</td><td>all checks on</td><td>Turn individual RPG checks on or off.</td></tr>
<tr><td><code>vanthrex.sourceDates.enabled</code></td><td>boolean</td><td><code>true</code></td><td>Read and save members <strong>with</strong> their sequence numbers and change dates (SRCSEQ/SRCDAT), like SEU. Unchanged lines keep their date; changed lines get today's date. Needs a Mapepire SQL engine; otherwise members are copied as plain text.</td></tr>
<tr><td><code>vanthrex.sourceDates.display</code></td><td>string</td><td><code>"date"</code></td><td>What to show in front of each member line (Ctrl+Alt+D cycles). Values: <code>date</code>, <code>seq-date</code>, <code>off</code>.</td></tr>
<tr><td><code>vanthrex.sourceDates.format</code></td><td>string</td><td><code>"yymmdd"</code></td><td>Date format: SEU-style YYMMDD or ISO YYYY-MM-DD. Values: <code>yymmdd</code>, <code>iso</code>.</td></tr>
<tr><td><code>vanthrex.conflictCheck</code></td><td>boolean</td><td><code>true</code></td><td>Warn when a member is locked by another job, or changed on the IBM i after you opened it, before your save overwrites it.</td></tr>
<tr><td><code>vanthrex.members.sortBy</code></td><td>string</td><td><code>"name"</code></td><td>Order of members in the Libraries view. Values: <code>name</code>, <code>date</code>.</td></tr>
<tr><td><code>vanthrex.sql.scriptStopOnError</code></td><td>boolean</td><td><code>true</code></td><td>Run SQL Script: stop at the first statement that fails (off = run every statement and report failures).</td></tr>
<tr><td><code>vanthrex.debug.port</code></td><td>number</td><td><code>0</code></td><td>IBM i Debug Service secured port. 0 = read it from the service configuration (usually 8005).</td></tr>
<tr><td><code>vanthrex.debug.ignoreCertificateErrors</code></td><td>boolean</td><td><code>false</code></td><td>Connect to the Debug Service even when its certificate cannot be verified. Only for test systems.</td></tr>
<tr><td><code>vanthrex.debug.updateProductionFiles</code></td><td>boolean</td><td><code>false</code></td><td>Allow the debugged program to update files in production libraries (UPDPROD).</td></tr>
<tr><td><code>vanthrex.debug.trace</code></td><td>boolean</td><td><code>false</code></td><td>Write a trace of the debug protocol to the IBM i Debug output (for support).</td></tr>
<tr><td><code>vanthrex.connections.keepOthersOpen</code></td><td>boolean</td><td><code>true</code></td><td>Keep other systems connected when you connect to another one, so you can switch between them instantly (Ctrl+Alt+S).</td></tr>
<tr><td><code>vanthrex.callGraph.depth</code></td><td>number</td><td><code>2</code></td><td>How many levels of callers / callees the call graph shows at first.</td></tr>
<tr><td><code>vanthrex.callGraph.maxNodes</code></td><td>number</td><td><code>200</code></td><td>Largest number of objects drawn in a call graph.</td></tr>
<tr><td><code>vanthrex.callGraph.hideSystemObjects</code></td><td>boolean</td><td><code>true</code></td><td>Leave IBM-supplied objects (QCMDEXC, QSYSPRT…) out of the call graph.</td></tr>
<tr><td><code>vanthrex.ai.enabled</code></td><td>boolean</td><td><code>true</code></td><td>Enable the @vanthrex AI assistant and the AI commands. Code you ask about is sent to the language model you selected in VS Code chat.</td></tr>
<tr><td><code>vanthrex.ai.useTools</code></td><td>boolean</td><td><code>true</code></td><td>Let the AI assistant look things up on the connected IBM i (object descriptions, table columns, source, read-only queries).</td></tr>
<tr><td><code>vanthrex.ai.allowQueries</code></td><td>boolean</td><td><code>true</code></td><td>Let the AI run read-only SQL queries (SELECT / WITH / VALUES only; anything that changes data is refused).</td></tr>
<tr><td><code>vanthrex.ai.confirmQueries</code></td><td>boolean</td><td><code>true</code></td><td>Ask before the AI runs a query on the IBM i.</td></tr>
<tr><td><code>vanthrex.ai.maxSourceChars</code></td><td>number</td><td><code>60000</code></td><td>Largest amount of source text sent to the language model in one request.</td></tr>
<tr><td><code>vanthrex.alerts.enabled</code></td><td>boolean</td><td><code>false</code></td><td>Show VS Code notifications when a job waits for a reply (MSGW), an inquiry arrives on QSYSOPR, a batch job ends abnormally or the system ASP passes the alert level.</td></tr>
<tr><td><code>vanthrex.alerts.intervalSeconds</code></td><td>number</td><td><code>60</code></td><td>How often live alerts check the IBM i, in seconds (30 or more).</td></tr>
<tr><td><code>vanthrex.alerts.scope</code></td><td>string</td><td><code>"mine"</code></td><td>Whose jobs and messages live alerts watch. Values: <code>mine</code>, <code>all</code>.</td></tr>
<tr><td><code>vanthrex.alerts.diskPercent</code></td><td>number</td><td><code>85</code></td><td>Alert when the system ASP is used above this percentage.</td></tr>
<tr><td><code>vanthrex.promotion.backupLibrary</code></td><td>string</td><td><code>"QGPL"</code></td><td>Library for the backup and transfer save files that object promotion creates.</td></tr>
<tr><td><code>vanthrex.export.maxRows</code></td><td>number</td><td><code>100000</code></td><td>Maximum number of rows exported to Excel, CSV or JSON.</td></tr>
<tr><td><code>vanthrex.performance.intervalSeconds</code></td><td>number</td><td><code>5</code></td><td>How often the performance monitor samples the IBM i, in seconds.</td></tr>
<tr><td><code>vanthrex.rpgunit.library</code></td><td>string</td><td><code>"RPGUNIT"</code></td><td>Library where RPGUnit (iRPGUnit) is installed; added to the library list to compile and run tests.</td></tr>
<tr><td><code>vanthrex.rpgunit.testLibrary</code></td><td>string</td><td><code>""</code></td><td>Library for the compiled test programs. Empty = your current library.</td></tr>
<tr><td><code>vanthrex.selfCheck.onConnect</code></td><td>boolean</td><td><code>true</code></td><td>Check the system the first time you connect to it in a session and warn about setup problems (SQL engine, CCSID, library list…).</td></tr>
<tr><td><code>vanthrex.spool.pdfMode</code></td><td>string</td><td><code>"local"</code></td><td>How spooled files become PDF: "local" converts the text in VS Code (works everywhere); "server" asks the IBM i (CPYSPLF WSCST(*PDF)) and keeps fonts and graphics, falling back to local. Values: <code>local</code>, <code>server</code>.</td></tr>
<tr><td><code>vanthrex.compare.maxRows</code></td><td>number</td><td><code>50000</code></td><td>Maximum rows read from each system when comparing a table across two systems.</td></tr>
<tr><td><code>vanthrex.ifs.followLines</code></td><td>number</td><td><code>500</code></td><td>How many lines at the end of a file "Follow File (tail -f)" shows; it refreshes every 2 seconds.</td></tr>
<tr><td><code>vanthrex.templates</code></td><td>array</td><td><code>[]</code></td><td>Your own templates for "New Member from Template…": name, source type (RPGLE, CLLE, SQL…), description and text. &amp;NAME, &amp;TEXT, &amp;DATE and &amp;USER are filled in.</td></tr>
<tr><td><code>vanthrex.scan.allowedLibraries</code></td><td>array</td><td><code>[]</code></td><td>Libraries that may be named in source without being reported by "Find Hard-Coded Libraries" (IBM libraries and QTEMP are always allowed).</td></tr>
<tr><td><code>vanthrex.pdm.userOptions</code></td><td>object</td><td><code>{}</code></td><td>PDM user-defined options (F16): option code → CL command. Variables: <code>&amp;L</code> library, <code>&amp;F</code> file, <code>&amp;N</code> name, <code>&amp;T</code> type, <code>&amp;A</code> attribute, <code>&amp;O</code> object library, <code>&amp;U</code> user, <code>&amp;X</code> text. Built-in: CB, CS, CC, DF, PF, RS (set one to an empty string to hide it).</td></tr>
<tr><td><code>vanthrex.compileOnSave</code></td><td>string</td><td><code>"off"</code></td><td>Compile a source member after you save it: <code>off</code>, <code>ask</code> (a notification with Compile / Always / Not now) or <code>always</code>. Copy members (INC, RPGLEINC…) are never compiled. Values: <code>off</code>, <code>ask</code>, <code>always</code>.</td></tr>
<tr><td><code>vanthrex.compileOnSave.types</code></td><td>array</td><td><code>[]</code></td><td>Only compile on save these source types (for example <code>RPGLE</code>, <code>SQLRPGLE</code>). Empty = every type that can be compiled.</td></tr>
<tr><td><code>vanthrex.memberStatusBar</code></td><td>boolean</td><td><code>true</code></td><td>Show, for the member you are editing, whether its program is up to date with the source and who else has it open (status bar; click for details).</td></tr>
<tr><td><code>vanthrex.connections.autoReconnect</code></td><td>boolean</td><td><code>true</code></td><td>When a connection drops (network, VPN, sleep), reconnect by itself with the saved sign-on: 5 attempts over about 2 minutes. Changes that could not be saved meanwhile are kept on this computer and saved when the system is back.</td></tr>
<tr><td><code>vanthrex.connections.healthCheckSeconds</code></td><td>number</td><td><code>60</code></td><td>Check every N seconds that the active system still answers (a tiny query). A slow answer shows in the status bar; two misses in a row reconnect. <code>0</code> turns it off.</td></tr>
<tr><td><code>vanthrex.notes.sharedFile</code></td><td>string</td><td><code>""</code></td><td>Share member notes with your team: an IFS file such as <code>/home/TEAM/vanthrex-notes.json</code> that everybody can read and write. Empty keeps notes on this computer only.</td></tr>
<tr><td><code>vanthrex.dsLayout.hover</code></td><td>boolean</td><td><code>true</code></td><td>Show the position and length of a data structure subfield when you hover over its definition.</td></tr>
<tr><td><code>vanthrex.5250.client</code></td><td>string</td><td><code>"auto"</code></td><td>Which program opens a 5250 session for the active system. Values: <code>auto</code>, <code>acs</code>, <code>tn5250</code>, <code>command</code>.</td></tr>
<tr><td><code>vanthrex.5250.acsPath</code></td><td>string</td><td><code>""</code></td><td>Path to acslaunch_win-64.exe, acslaunch_linux-64, the ACS app or acsbundle.jar (empty: found automatically).</td></tr>
<tr><td><code>vanthrex.5250.command</code></td><td>string</td><td><code>""</code></td><td>Command that starts your 5250 emulator, with <code>${host}</code>, <code>${user}</code>, <code>${device}</code> and <code>${port}</code> replaced, for example <code>"C:\\Program Files\\IBM\\Client Access\\Emulator\\pcsws.exe" /H=${host}</code>.</td></tr>
<tr><td><code>vanthrex.5250.deviceName</code></td><td>string</td><td><code>""</code></td><td>Display device name to use (tn5250 and your own command).</td></tr>
<tr><td><code>vanthrex.5250.ssl</code></td><td>boolean</td><td><code>false</code></td><td>Use TLS (port 992) for tn5250.</td></tr>
<tr><td><code>vanthrex.5250.port</code></td><td>number</td><td><code>0</code></td><td>Telnet port when it is not the default (23, or 992 with TLS).</td></tr>
<tr><td><code>vanthrex.deploy.directory</code></td><td>string</td><td><code>""</code></td><td>IFS folder a local workspace folder is deployed to. <code>${home}</code>, <code>${user}</code> and <code>${folder}</code> are replaced. Empty: <code>${home}/builds/${folder}</code>.</td></tr>
<tr><td><code>vanthrex.deploy.ignore</code></td><td>array</td><td><code>["node_modules/", ".vscode/", "*.vsix", "*.log", ".env", ".env.*", "*.pem", "*.key"]</code></td><td>Files and folders that are never deployed (<code>*</code> and <code>**</code> wildcards, a trailing <code>/</code> for folders). <code>.git</code> is always skipped.</td></tr>
<tr><td><code>vanthrex.deploy.buildCommand</code></td><td>string</td><td><code>""</code></td><td>Command <strong>Build Project on IBM i</strong> runs in PASE in the deploy folder, for example <code>makei build</code> (Bob) or <code>gmake</code>. <code>CURLIB</code> and <code>LIBL</code> are set from the connection.</td></tr>
<tr><td><code>vanthrex.deploy.ccsid</code></td><td>number</td><td><code>1208</code></td><td>CCSID the deployed files are tagged with (1208 = UTF-8, so compilers read them correctly). 0 leaves the tag alone.</td></tr>
<tr><td><code>vanthrex.deploy.onSave</code></td><td>boolean</td><td><code>false</code></td><td>Upload a local file to its deploy folder every time it is saved.</td></tr>
<tr><td><code>vanthrex.deploy.compileDeploysChanges</code></td><td>boolean</td><td><code>true</code></td><td>Before compiling a local file, deploy every changed file of the folder too (so changed copybooks and includes are used).</td></tr>
<tr><td><code>vanthrex.terminal.openSourcePath</code></td><td>boolean</td><td><code>true</code></td><td>Put <code>/QOpenSys/pkgs/bin</code> (yum open-source tools: bash, git, python…) first on the PATH of a new PASE terminal.</td></tr>
<tr><td><code>vanthrex.notebook.maxRows</code></td><td>number</td><td><code>1000</code></td><td>Rows an SQL cell of an IBM i notebook reads (a cell can ask for more with <code>-- rows: N</code>).</td></tr>
<tr><td><code>vanthrex.editor.columnHints</code></td><td>boolean</td><td><code>true</code></td><td>Show the fixed-format field under the cursor (RPG and DDS) in the status bar.</td></tr>
<tr><td><code>vanthrex.editor.rpgIndent</code></td><td>number</td><td><code>2</code></td><td>Spaces per level when <strong>Format Document</strong> re-indents fully free RPG.</td></tr>
<tr><td><code>vanthrex.editor.clCommandHelp</code></td><td>boolean</td><td><code>true</code></td><td>In CL sources, show what a command does when you hover it and offer its keywords and allowed values while typing (read from the command definitions on the connected system).</td></tr>
<tr><td><code>vanthrex.editor.sqlCodeLens</code></td><td>boolean</td><td><code>true</code></td><td>Show <strong>Run</strong>, <strong>Explain</strong> and <strong>RPG code</strong> links above each statement of an SQL file.</td></tr>
<tr><td><code>vanthrex.codeGen.arraySize</code></td><td>number</td><td><code>100</code></td><td>Number of elements (<code>dim</code>) of arrays in generated RPG (JSON arrays, rows read per FETCH).</td></tr>
<tr><td><code>vanthrex.codeGen.insertRows</code></td><td>number</td><td><code>1000</code></td><td>Rows <strong>Copy Rows as SQL INSERT Script</strong> reads at most.</td></tr>
<tr><td><code>vanthrex.ai.redact.secrets</code></td><td>boolean</td><td><code>true</code></td><td>Before anything is sent to the AI, replace passwords (CL <code>PASSWORD(…)</code>, <code>pwd = …</code>), API keys, tokens, private keys and credentials in URLs by placeholders (xxxx1, xxxx2…). The real values are put back only on this computer, in the answer.</td></tr>
<tr><td><code>vanthrex.ai.redact.personalData</code></td><td>boolean</td><td><code>true</code></td><td>Replace e-mail addresses, payment card numbers (Luhn-checked) and IBANs (checksum-checked) by placeholders before they are sent to the AI.</td></tr>
<tr><td><code>vanthrex.ai.redact.hostNames</code></td><td>boolean</td><td><code>true</code></td><td>Replace IP addresses and the host names of your connections (and of <code>vanthrex.ai.redact.hostList</code>) by placeholders before they are sent to the AI.</td></tr>
<tr><td><code>vanthrex.ai.redact.hostList</code></td><td>array</td><td><code>[]</code></td><td>More internal host or server names to hide from the AI.</td></tr>
<tr><td><code>vanthrex.ai.redact.words</code></td><td>array</td><td><code>[]</code></td><td>Words that must never be sent to the AI (customer names, project code names…): replaced by placeholders.</td></tr>
<tr><td><code>vanthrex.ai.sensitiveColumns</code></td><td>array</td><td><code>["PASS", "PWD", "SECRET", "TOKEN", "APIKEY", "SSN", "SOCSEC", "NIR", "IBAN", "BIC", "SWIFT", "CARD", "CCNUM", "CVV", "PAN", "SALARY", "SALAIRE", "WAGE", "PAYRATE", "BIRTH", "DOB", "TAXID", "NATID", "PASSPORT", "EMAIL", "MAIL", "PHONE", "TEL", "MOBILE", "ADDRESS", "ADR"]</code></td><td>Columns whose values are always replaced by <code>xxxx</code> in query results sent to the AI (a column matches when its name contains the word; short words must be a whole part of the name).</td></tr>
<tr><td><code>vanthrex.ai.deniedLibraries</code></td><td>array</td><td><code>[]</code></td><td>Libraries the AI may never read (source, objects, queries, authorities). <code>PAY*</code> matches every library starting with PAY.</td></tr>
<tr><td><code>vanthrex.ai.productionData</code></td><td>string</td><td><code>"metadata"</code></td><td>What the AI may read on <strong>protected</strong> connections (production protection <em>Confirm</em> or <em>Read-only</em>): <code>metadata</code> = source, catalog and object facts but no table rows (default), <code>full</code> = also query results (masked), <code>none</code> = nothing. Values: <code>full</code>, <code>metadata</code>, <code>none</code>.</td></tr>
<tr><td><code>vanthrex.ai.otherSystemsData</code></td><td>string</td><td><code>"full"</code></td><td>What the AI may read on connections that are not protected: <code>full</code> (query results are still masked), <code>metadata</code> or <code>none</code>. Values: <code>full</code>, <code>metadata</code>, <code>none</code>.</td></tr>
<tr><td><code>vanthrex.ai.audit</code></td><td>boolean</td><td><code>true</code></td><td>Keep an audit trail of what is sent to the AI (time, system, feature, size, number of hidden values — never the content) in the <em>Vanthrex AI Audit</em> output and a file in the extension's storage.</td></tr>
<tr><td><code>vanthrex.ai.showPrivacyNote</code></td><td>boolean</td><td><code>true</code></td><td>After an answer, say how many values were hidden from the AI.</td></tr>
<tr><td><code>vanthrex.ai.codeLens</code></td><td>boolean</td><td><code>true</code></td><td>Show ✨ <strong>Explain · Document · Tests</strong> above each RPG procedure and subroutine.</td></tr>
<tr><td><code>vanthrex.ai.modelFamily</code></td><td>string</td><td><code>""</code></td><td>Language model family for <strong>AI: Change the Selected Code</strong> (for example <code>gpt-4o</code> or <code>claude-sonnet-4</code>); empty = the first available model. The chat uses the model chosen in the chat window.</td></tr>
<tr><td><code>vanthrex.editor.checkCharacters</code></td><td>boolean</td><td><code>true</code></td><td>Underline characters that break a compile or a CCSID conversion (tabs, control characters, no-break spaces, curly quotes, characters lost in a conversion) when a source is opened or saved.</td></tr>
<tr><td><code>vanthrex.csvSeparator</code></td><td>string</td><td><code>","</code></td><td>Separator of CSV files written by <strong>Report to CSV</strong> (<code>;</code> for spreadsheets set up for a comma as decimal separator). Values: <code>,</code>, <code>;</code>, <code>	</code>.</td></tr>
<tr><td><code>vanthrex.jobHistoryDays</code></td><td>number</td><td><code>30</code></td><td>Days of history log read by <strong>Job Run History</strong>.</td></tr>
<tr><td><code>vanthrex.unusedIndexDays</code></td><td>number</td><td><code>180</code></td><td>Days without query use or open before <strong>Unused Indexes</strong> proposes an index.</td></tr>
<tr><td><code>vanthrex.spoolSearchDays</code></td><td>number</td><td><code>7</code></td><td>Days of spooled files searched by <strong>Find a Text in Spooled Files</strong>.</td></tr>
<tr><td><code>vanthrex.editor.matchBlocks</code></td><td>boolean</td><td><code>true</code></td><td>Highlight the matching IF / ELSE / ENDIF, DO / ENDDO, SELECT / WHEN / ENDSL keywords in RPG and CL when the cursor is on one.</td></tr>
<tr><td><code>vanthrex.editor.explainCodes</code></td><td>boolean</td><td><code>true</code></td><td>Explain SQLCODE, SQLSTATE and RPG status codes (01218, -803, '23505') when hovering them in RPG, SQL and CL.</td></tr>
<tr><td><code>vanthrex.editor.changeLogTemplate</code></td><td>string</td><td><code>"{date} {user} {ticket} {text}"</code></td><td>Text of <strong>Add Change Log Entry</strong>: <code>{date}</code>, <code>{user}</code>, <code>{ticket}</code>, <code>{text}</code>. Use <code>\n</code> for more lines.</td></tr>
<tr><td><code>vanthrex.editor.changeLogUser</code></td><td>string</td><td><code>""</code></td><td>Name written by <strong>Add Change Log Entry</strong> (empty: the IBM i user of the connection).</td></tr>
<tr><td><code>vanthrex.profileSampleRows</code></td><td>number</td><td><code>0</code></td><td><strong>Data Profile</strong>: read only the first N rows (0 = the whole table).</td></tr>
<tr><td><code>vanthrex.capacityWarnPercent</code></td><td>number</td><td><code>80</code></td><td><strong>Columns Close to Their Limit</strong> marks columns that use this percentage of what they can hold.</td></tr>
<tr><td><code>vanthrex.unusedObjectDays</code></td><td>number</td><td><code>365</code></td><td>Days without use before <strong>Unused Objects</strong> lists an object.</td></tr>
<tr><td><code>vanthrex.benchmarkRows</code></td><td>number</td><td><code>1000</code></td><td>Rows fetched on each run by <strong>Time This SQL Statement</strong>.</td></tr>
<tr><td><code>vanthrex.scheduleDays</code></td><td>number</td><td><code>7</code></td><td>Days shown by <strong>Job Schedule for the Next Days</strong>.</td></tr>
<tr><td><code>vanthrex.memberCache.enabled</code></td><td>boolean</td><td><code>true</code></td><td>Keep members you open on this computer: a member that did not change on the IBM i opens again instantly (one small query instead of a copy).</td></tr>
<tr><td><code>vanthrex.memberCache.maxMembers</code></td><td>number</td><td><code>500</code></td><td>Members kept by the member cache (the least recently used are removed).</td></tr>
<tr><td><code>vanthrex.index.membersPerTrip</code></td><td>number</td><td><code>150</code></td><td>Members read in one round trip when indexing sources.</td></tr>
<tr><td><code>vanthrex.index.parallel</code></td><td>number</td><td><code>3</code></td><td>Source files read at the same time when indexing sources.</td></tr>
<tr><td><code>vanthrex.index.refreshOnConnect</code></td><td>boolean</td><td><code>true</code></td><td>After connecting, read again the indexed members that changed (in the background).</td></tr>
<tr><td><code>vanthrex.goTo.maxItems</code></td><td>number</td><td><code>40000</code></td><td>Most members and objects listed by <strong>Go to Anything</strong>.</td></tr>
<tr><td><code>vanthrex.goTo.refreshMinutes</code></td><td>number</td><td><code>30</code></td><td>Minutes before <strong>Go to Anything</strong> reloads its list in the background.</td></tr>
<tr><td><code>vanthrex.warmUp.enabled</code></td><td>boolean</td><td><code>true</code></td><td>After connecting, prepare in the background: the SQL job, the Go to Anything list, the source index and the most recent members.</td></tr>
<tr><td><code>vanthrex.warmUp.members</code></td><td>number</td><td><code>5</code></td><td>Recently opened members loaded into the member cache by the warm-up.</td></tr>
<tr><td><code>vanthrex.compile.parallel</code></td><td>number</td><td><code>4</code></td><td>Members compiled at the same time by Batch Compile and Recompile the Programs That Use This File (1 = one after the other).</td></tr>
<tr><td><code>vanthrex.editor.referenceLinks</code></td><td>boolean</td><td><code>true</code></td><td>Make IBM i references clickable in sources, spooled files and logs: LIB/FILE(MBR), PGM(LIB/OBJ), IFS paths, message IDs and job names.</td></tr>
<tr><td><code>vanthrex.macros</code></td><td>array</td><td><code>[]</code></td><td>CL macros for <strong>Run a CL Macro</strong>: a name and a list of CL commands. <code>${NAME}</code> asks for a value when the macro runs (<code>${LIB:MYLIB}</code> with a default); <code>${USER}</code>, <code>${CURLIB}</code>, <code>${DATE}</code> and <code>${TIME}</code> are filled in. The commands run in order and stop at the first error.</td></tr>
<tr><td><code>vanthrex.editor.fileFieldHelp</code></td><td>boolean</td><td><code>true</code></td><td>In RPG, hovering a declared file shows its fields from Db2, hovering a field shows its type and text, field names are completed and Ctrl+click on a file opens its DDS source.</td></tr>
<tr><td><code>vanthrex.editor.autoCloseBlocks</code></td><td>boolean</td><td><code>true</code></td><td>In RPG, pressing Enter after <code>IF</code>, <code>DOW</code>, <code>FOR</code>, <code>SELECT</code>, <code>MONITOR</code>, <code>BEGSR</code> or <code>DCL-PROC</code> adds the matching <code>END…</code> line when it is missing.</td></tr>
<tr><td><code>vanthrex.editor.parameterNameHints</code></td><td>boolean</td><td><code>true</code></td><td>In RPG, shows the parameter names before the arguments of procedure calls (inlay hints).</td></tr>
<tr><td><code>vanthrex.editor.referenceCodeLens</code></td><td>boolean</td><td><code>false</code></td><td>In RPG, shows the number of references above each procedure and subroutine.</td></tr>
<tr><td><code>vanthrex.editor.localCompletion</code></td><td>boolean</td><td><code>true</code></td><td>In RPG, completes the names declared in the source: variables, constants, procedures (with their parameters) and subroutines after <code>EXSR</code>.</td></tr>
<tr><td><code>vanthrex.editor.procedureInStatusBar</code></td><td>boolean</td><td><code>true</code></td><td>In RPG, shows the procedure or subroutine the cursor is in, in the status bar.</td></tr>
<tr><td><code>vanthrex.editor.fixedColumnHighlight</code></td><td>boolean</td><td><code>true</code></td><td>In fixed-format RPG, shades every other column field of the current line and shows its name on hover.</td></tr>
<tr><td><code>vanthrex.editor.wrapColumn</code></td><td>number</td><td><code>100</code></td><td>Column at which <strong>Wrap Long Line</strong> splits free-form RPG. Column-limited sources always wrap at 80.</td></tr>
<tr><td><code>vanthrex.editor.docsRelease</code></td><td>string</td><td><code>"7.5"</code></td><td>IBM i release used by <strong>Open IBM Documentation for the Word</strong>.</td></tr>
<tr><td><code>vanthrex.lint.maxNesting</code></td><td>number</td><td><code>6</code></td><td>Deepest block nesting before the <code>deep-nesting</code> check reports it.</td></tr>
<tr><td><code>vanthrex.editor.inlineSuggestions</code></td><td>boolean</td><td><code>true</code></td><td>Suggestions while you type in RPG and CL, shown in grey and accepted with <strong>Tab</strong>: the next statement you usually write (IF %FOUND after CHAIN, SQLCODE test after embedded SQL, OPEN and FETCH after DECLARE CURSOR, MONMSG after CHKOBJ / DLTF…), the type of a new variable from its name and from the variables already declared, the file of %FOUND / %EOF and the parameters of a call. Offline: nothing is sent anywhere.</td></tr>
<tr><td><code>vanthrex.ai.inlineSuggestions</code></td><td>boolean</td><td><code>false</code></td><td>Also ask the AI model for a suggestion when you pause typing and no offline suggestion applies (RPG, CL, SQL, DDS). The code around the cursor goes through the Vanthrex guard first (secrets and personal data replaced, denied libraries and protected systems never sent) and every request is in the audit trail.</td></tr>
<tr><td><code>vanthrex.ai.inlineDelay</code></td><td>number</td><td><code>500</code></td><td>Pause in milliseconds before an AI suggestion is requested.</td></tr>
<tr><td><code>vanthrex.lint.cl</code></td><td>boolean</td><td><code>true</code></td><td>Check CL sources while you type: undeclared and unused variables, GOTO to a missing label, DO / SELECT / SUBR not closed, DCL after the first command, literals too long, text in *DEC variables, hard-coded libraries.</td></tr>
<tr><td><code>vanthrex.lint.sql</code></td><td>boolean</td><td><code>true</code></td><td>Check SQL scripts while you type: UPDATE / DELETE without WHERE, DROP / TRUNCATE, = NULL instead of IS NULL, SELECT INTO without WHERE.</td></tr>
<tr><td><code>vanthrex.editor.toolboxButton</code></td><td>boolean</td><td><code>true</code></td><td>Show the <strong>$(tools) IBM i</strong> button in the status bar for RPG, CL, SQL and DDS sources: it opens the tools that fit the file and the selection (also <strong>Ctrl+Alt+A</strong>).</td></tr>
<tr><td><code>vanthrex.editor.sizeHovers</code></td><td>boolean</td><td><code>true</code></td><td>Hovering a literal shows its length (bytes for X'…' hex literals); hovering a declared RPG variable shows its storage size.</td></tr>
<tr><td><code>vanthrex.standards</code></td><td>object</td><td><code>{}</code></td><td>Team coding standards for RPG, checked while you type and in the Code Health Report. All off by default; set them with <strong>Team Coding Standards…</strong> or import an <strong>rpglint.json</strong>. Put them in the workspace settings so the whole team uses the same ones.</td></tr>
<tr><td><code>vanthrex.lint.dds</code></td><td>boolean</td><td><code>true</code></td><td>Check DDS sources (PF, LF, DSPF, PRTF) while you type: names longer than 10 characters, duplicate fields or record formats, missing lengths, decimals and length limits, key fields not in the record, display fields outside the screen or on top of each other.</td></tr>
<tr><td><code>vanthrex.editor.semanticHighlighting</code></td><td>boolean</td><td><code>true</code></td><td>Colour RPG names by what they are: parameters, constants (read-only), data structures and subfields, procedures, files and subroutines; globals used inside a procedure are marked.</td></tr>
<tr><td><code>vanthrex.editor.indentOnType</code></td><td>boolean</td><td><code>true</code></td><td>In free-form RPG, typing the <code>;</code> of ENDIF, ENDDO, ELSE, WHEN, END-PROC… moves the line to the indentation of its opener.</td></tr>
<tr><td><code>vanthrex.editor.terminalLinks</code></td><td>boolean</td><td><code>true</code></td><td>In every terminal, LIB/FILE(MEMBER), message IDs (CPF9801, MCH1210…) and IFS paths become links: click to open the member or file, or explain the message.</td></tr>
<tr><td><code>vanthrex.sharedSnippets.folder</code></td><td>string</td><td><code>""</code></td><td>IFS folder of shared snippets: set it to a folder your team can write to, for example /shared/vanthrex/snippets, so everyone sees the same snippets. {user} is replaced by the user profile. Empty: /home/{user}/.vanthrex/snippets (only yours).</td></tr>
<tr><td><code>vanthrex.backupDays</code></td><td>number</td><td><code>7</code></td><td>Days after which <strong>Backup Freshness</strong> marks a library as not saved lately.</td></tr>
</tbody>
</table>

## RPG check rules

Use `vanthrex.lint.rules` to switch single checks off, for example:

```json
"vanthrex.lint.rules": { "numbered-indicator": false, "select-star": false }
```

| Rule | What it reports |
|---|---|
| `unused-definition` | Variables, constants and subroutines that are declared but never used |
| `goto` | GOTO usage |
| `tag` | TAG labels |
| `program-end` | Main program without *INLR = *ON or RETURN |
| `long-procedure` | Procedures longer than the configured number of lines |
| `numbered-indicator` | Numbered indicators (*IN01-*IN99) |
| `empty-on-error` | ON-ERROR blocks that silently swallow errors |
| `select-star` | SELECT * in embedded SQL |
| `mixed-format` | Fixed-format calculation specs in a free-format source |

## Compile actions

These are the built-in entries of `vanthrex.compileActions`. Copy one into your settings to change it, or add your own.

Variables: `&LIB` (source library), `&OBJLIB` (object library), `&SRCFILE`, `&NAME`, `&EXT`, `&FULLPATH` (IFS path), `&CURLIB`, `&USER`.

| Name | Source types | From | Command |
|---|---|---|---|
| Create Bound RPG Program (CRTBNDRPG) | rpgle | member | `CRTBNDRPG PGM(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)` |
| Create RPG Module (CRTRPGMOD) | rpgle | member | `CRTRPGMOD MODULE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)` |
| Create SQL RPG Program (CRTSQLRPGI) | sqlrpgle | member | `CRTSQLRPGI OBJ(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OBJTYPE(*PGM) COMMIT(*NONE) OPTION(*EVENTF) DBGVIEW(*SOURCE) CLOSQLCSR(*ENDMOD) REPLACE(*YES)` |
| Create Bound CL Program (CRTBNDCL) | clle | member | `CRTBNDCL PGM(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)` |
| Create CL Program (CRTCLPGM) | clp | member | `CRTCLPGM PGM(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) REPLACE(*YES)` |
| Create Command (CRTCMD) | cmd | member | `CRTCMD CMD(&OBJLIB/&NAME) PGM(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) REPLACE(*YES)` |
| Create Physical File (CRTPF) | pf | member | `CRTPF FILE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF)` |
| Create Logical File (CRTLF) | lf | member | `CRTLF FILE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF)` |
| Create Display File (CRTDSPF) | dspf | member | `CRTDSPF FILE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) REPLACE(*YES)` |
| Create Printer File (CRTPRTF) | prtf | member | `CRTPRTF FILE(&OBJLIB/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) REPLACE(*YES)` |
| Run SQL Script (RUNSQLSTM) | sql | member | `RUNSQLSTM SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) COMMIT(*NONE) NAMING(*SQL)` |
| Create Bound RPG Program from IFS (CRTBNDRPG) | rpgle | ifs | `CRTBNDRPG PGM(&OBJLIB/&NAME) SRCSTMF('&FULLPATH') OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES) TGTCCSID(*JOB)` |
| Create SQL RPG Program from IFS (CRTSQLRPGI) | sqlrpgle | ifs | `CRTSQLRPGI OBJ(&OBJLIB/&NAME) SRCSTMF('&FULLPATH') OBJTYPE(*PGM) COMMIT(*NONE) OPTION(*EVENTF) DBGVIEW(*SOURCE) CVTCCSID(*JOB) REPLACE(*YES)` |
| Create Bound CL Program from IFS (CRTBNDCL) | clle | ifs | `CRTBNDCL PGM(&OBJLIB/&NAME) SRCSTMF('&FULLPATH') OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)` |
| Run SQL Script from IFS (RUNSQLSTM) | sql | ifs | `RUNSQLSTM SRCSTMF('&FULLPATH') COMMIT(*NONE) NAMING(*SQL)` |

```json
"vanthrex.compileActions": [
  {
    "name": "Create RPG program into my test library",
    "extensions": ["rpgle"],
    "source": "member",
    "command": "CRTBNDRPG PGM(MYTEST/&NAME) SRCFILE(&LIB/&SRCFILE) SRCMBR(&NAME) OPTION(*EVENTF) DBGVIEW(*SOURCE) REPLACE(*YES)"
  }
]
```

Keep `OPTION(*EVENTF)` so the errors can be shown inline.
