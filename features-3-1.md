---
layout: default
title: "New in 3.1"
parent: "What's new"
nav_order: 3
---

# New in 3.1
{: .no_toc }

More power in the editor: DDS checks, CL formatting, RPG semantic highlighting, names edited together, END lines indented as you type, links to a line and clickable terminal output.
{: .fs-6 .fw-300 }

1. TOC
{:toc}

## What is new

![DDS checks while you type]({{ "/images/dds-checks.png" | relative_url }})
*DDS checks while you type: decimals, fields outside the screen, names declared twice, overlapping fields, missing lengths.*

![Format Document for CL]({{ "/images/cl-format-compare.png" | relative_url }})
*Format Document for CL puts labels, commands and parameters in the prompter columns and splits long commands with +.*


- **DDS checks while you type** (PF, LF, DSPF, PRTF; `vanthrex.lint.dds`): names longer than 10 characters, a field or record format declared twice, fields with no length (and no reference), more decimals than the length, lengths beyond the data type, key fields that are not in the record, display fields or constants outside the screen (DSPSIZ, *DS3 / *DS4) and display fields on top of each other. Reference fields, logical files and conditioned fields are left alone. DDS members are part of the Code Health Report too.
- **Format Document for CL** (Shift+Alt+F): the prompter layout — labels in column 1, commands in column 14, parameters from column 25, long commands split with `+` before column 80. Statements with a comment inside are kept as they are.
- **RPG semantic highlighting** (`vanthrex.editor.semanticHighlighting`): parameters, constants and CONST parameters (read-only), data structures and subfields, procedures, files and subroutines each get their own colour, and a global variable used inside a procedure is marked — on top of the existing syntax colours.
- **Names edited together**: renaming a procedure or a data structure on its `DCL-PROC` / `DCL-DS` line changes the name on its `END-PROC` / `END-DS` line at the same time, and the other way round.
- **END lines indented as you type** (`vanthrex.editor.indentOnType`): typing the `;` of ENDIF, ENDDO, ELSE, WHEN, OTHER, ON-ERROR, END-PROC… moves the line under its opener.
- **Links that open a member at a line**: *Copy a Link That Opens This Line* (right-click, or Ctrl+Alt+A → Copy) gives a `vscode://…` link for tickets, chats and e-mails; whoever clicks it, with Vanthrex installed, opens the same member (or IFS file) at the same line, on the named system after a confirmation.
- **Clickable IBM i references in every terminal** (`vanthrex.editor.terminalLinks`): `LIB/FILE(MEMBER)` opens the member, message IDs such as `CPF9801` or `MCH1210` are explained, IFS paths open the file — in the PASE terminal, build output, and any other terminal.

## Settings

| Setting | Default | What it does |
|---|---|---|
| `vanthrex.lint.dds` | on | DDS checks while you type |
| `vanthrex.editor.semanticHighlighting` | on | RPG names coloured by what they are |
| `vanthrex.editor.indentOnType` | on | END / ELSE / WHEN lines moved under their opener |
| `vanthrex.editor.terminalLinks` | on | Members, message IDs and IFS paths clickable in terminals |

Each DDS check can also be turned off in `vanthrex.lint.rules`.

## Examples

<div class="showcase"><div class="showcase-text"><h3>DDS checks while you type</h3><p>Physical, logical, display and printer files are checked as you type; each finding names its rule, so you can turn it off.</p></div><div class="showcase-demo"><div class="demo"><div class="demo-bar"><span class="dots"><i></i><i></i><i></i></span><span class="file">CUSTDSP.dspf</span></div><pre class="demo-code"><span class="line">     A                                      DSPSIZ(<span class="n">24</span> <span class="n">80</span> <span class="sp">*DS</span>3)</span><span class="line">     A          R CUSTSCREEN</span><span class="line">     A            CUSTNO         7Y 0B  <span class="n">3</span> <span class="n">20</span></span><span class="line">     A            CUSTNAME      40A  O  <span class="n">3</span> <span class="warn"><span class="n">24</span></span></span><span class="line">     A            AMOUNT         5Y <span class="err"><span class="n">7</span></span>O  <span class="n">5</span> <span class="n">20</span></span><span class="line">     A            COMMENT       30A  O  <span class="n">7</span> <span class="err"><span class="n">60</span></span></span></pre><div class="demo-problems"><div class="demo-problems-title">Problems</div><div class="demo-msg"><span class="ico w">!</span><span class="t">CUSTNAME overlaps CUSTNO (line 4) on screen line 3.</span><span class="r">dds-overlap</span></div><div class="demo-msg"><span class="ico e">✕</span><span class="t">AMOUNT has 7 decimal positions but a length of 5.</span><span class="r">dds-decimals</span></div><div class="demo-msg"><span class="ico e">✕</span><span class="t">COMMENT at line 7 position 60 (length 30) does not fit on a 24 × 80 screen.</span><span class="r">dds-off-screen</span></div></div></div></div></div>
<div class="showcase"><div class="showcase-text"><h3>Format Document for CL</h3><p>Press <kbd>Shift+Alt+F</kbd>: labels, commands and parameters go to the prompter columns and long commands are split with <code>+</code>.</p></div><div class="showcase-demo"><div class="before-after"><div><div class="ba-label">Before</div><div class="demo"><div class="demo-bar"><span class="dots"><i></i><i></i><i></i></span><span class="file">MONTHEND.clle</span></div><pre class="demo-code"><span class="line"><span class="k">PGM</span> <span class="k">PARM</span>(<span class="v">&amp;LIB</span>)</span><span class="line"><span class="k">DCL</span> <span class="k">VAR</span>(<span class="v">&amp;LIB</span>) <span class="k">TYPE</span>(<span class="sp">*CHAR</span>) <span class="k">LEN</span>(<span class="n">10</span>)</span><span class="line">START: <span class="k">CHKOBJ</span> <span class="k">OBJ</span>(<span class="v">&amp;LIB</span>/ORDERS) <span class="k">OBJTYPE</span>(<span class="sp">*FILE</span>)</span><span class="line"><span class="k">MONMSG</span> <span class="k">MSGID</span>(CPF9801) <span class="k">EXEC</span>(<span class="k">GOTO</span> <span class="k">CMDLBL</span>(END))</span><span class="line"><span class="k">CPYF</span> <span class="k">FROMFILE</span>(<span class="v">&amp;LIB</span>/ORDERS) <span class="k">TOFILE</span>(QTEMP/ORDERS) <span class="k">MBROPT</span>(<span class="sp">*REPLACE</span>) <span class="k">CRTFILE</span>(<span class="sp">*YES</span>)</span><span class="line">END: <span class="k">ENDPGM</span></span></pre></div></div><div><div class="ba-label after">After</div><div class="demo"><div class="demo-bar"><span class="dots"><i></i><i></i><i></i></span><span class="file">MONTHEND.clle</span><span class="label">Shift+Alt+F</span></div><pre class="demo-code"><span class="line">             <span class="k">PGM</span>        <span class="k">PARM</span>(<span class="v">&amp;LIB</span>)</span><span class="line">             <span class="k">DCL</span>        <span class="k">VAR</span>(<span class="v">&amp;LIB</span>) <span class="k">TYPE</span>(<span class="sp">*CHAR</span>) <span class="k">LEN</span>(<span class="n">10</span>)</span><span class="line">START:       <span class="k">CHKOBJ</span>     <span class="k">OBJ</span>(<span class="v">&amp;LIB</span>/ORDERS) <span class="k">OBJTYPE</span>(<span class="sp">*FILE</span>)</span><span class="line">             <span class="k">MONMSG</span>     <span class="k">MSGID</span>(CPF9801) <span class="k">EXEC</span>(<span class="k">GOTO</span> <span class="k">CMDLBL</span>(END))</span><span class="line">             <span class="k">CPYF</span>       <span class="k">FROMFILE</span>(<span class="v">&amp;LIB</span>/ORDERS) <span class="k">TOFILE</span>(QTEMP/ORDERS) +</span><span class="line">                          <span class="k">MBROPT</span>(<span class="sp">*REPLACE</span>) <span class="k">CRTFILE</span>(<span class="sp">*YES</span>)</span><span class="line">END:         <span class="k">ENDPGM</span></span></pre></div></div></div></div></div>
<div class="showcase"><div class="showcase-text"><h3>A link that opens a line</h3><p>Right-click → <strong>Copy a Link That Opens This Line</strong>, or <kbd>Ctrl+Alt+A</kbd> → Copy. Whoever clicks it opens the same member at the same line.</p></div><div class="showcase-demo"><div class="demo"><div class="demo-bar"><span class="dots"><i></i><i></i><i></i></span><span class="file">Copy a Link That Opens This Line</span><span class="label">paste it in a ticket or a chat</span></div><pre class="demo-code"><span class="line">vscode:<span class="c">//gauravgupta0612.vanthrex-ibmi/open?system=DEV400&amp;member=APPLIB%2FQRPGLESRC%2FORDERS&amp;type=rpgle&amp;line=19</span></span></pre></div></div></div>
<div class="showcase"><div class="showcase-text"><h3>Clickable terminals</h3><p><kbd>Ctrl</kbd>+click a member to open it, a message ID to read its explanation, an IFS path to open the file.</p></div><div class="showcase-demo"><div class="demo"><div class="demo-bar"><span class="dots"><i></i><i></i><i></i></span><span class="file">Terminal</span><span class="label">Ctrl+click to open or explain</span></div><pre class="demo-code"><span class="line">&gt; CRTBNDRPG PGM(APPLIB/ORDERS) SRCFILE(<span class="sel">APPLIB/QRPGLESRC(ORDERS)</span>)</span><span class="line">  <span class="sel">RNF7030</span> The name or indicator CUSTNAM is not defined.</span><span class="line">  See <span class="sel">/home/dev/build/orders.log</span> for details.</span></pre></div></div></div>
