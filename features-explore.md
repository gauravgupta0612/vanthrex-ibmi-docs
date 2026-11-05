---
layout: default
title: "Connect & explore"
parent: "Features"
nav_order: 1
has_children: true
has_toc: false
---

# Connect & explore

Connect to one or several IBM i systems and find your way around them.
{: .fs-6 .fw-300 }

![A guided form to connect, with Test connection.]({{ "/images/add-connection.png" | relative_url }})
*A guided form to connect, with Test connection.*

| Page | What you get |
|---|---|
| [Connect & browse](features-connect-browse.md) | Connections (several systems at once), libraries, source files, members, objects and the IFS. |
| [PDM in one screen](features-pdm.md) | WRKLIBPDM, WRKOBJPDM and WRKMBRPDM in one view: option numbers, F-keys, subset, user-defined options. |
| [Object tools](features-object-tools.md) | Object information, who has an object locked, compare two libraries, modules and exports. |
| [System Tracker](features-tracker.md) | The whole system in one page: what needs attention, libraries, jobs, storage, QSYSOPR, users, PTFs. |
| [See and share](features-see-share.md) | 5250 screen preview, database diagrams, compare two systems, spooled files to PDF and e-mail. |
| [IFS Space Map](features-3-2.md#ifs-space-map) *(3.2)* | Folders and files below an IFS folder as a treemap; click to go in. |

## Examples

<div class="showcase"><div class="showcase-text"><h3>Share a line with a link</h3><p>Paste the link in a ticket, a chat or an e-mail: it opens the same member at the same line, on the named system after a confirmation.</p><p><a href="{{ "/features-3-1.html" | relative_url }}">Read more →</a></p></div><div class="showcase-demo"><div class="demo"><div class="demo-bar"><span class="dots"><i></i><i></i><i></i></span><span class="file">Copy a Link That Opens This Line</span><span class="label">paste it in a ticket or a chat</span></div><pre class="demo-code"><span class="line">vscode:<span class="c">//gauravgupta0612.vanthrex-ibmi/open?system=DEV400&amp;member=APPLIB%2FQRPGLESRC%2FORDERS&amp;type=rpgle&amp;line=19</span></span></pre></div></div></div>
<div class="showcase"><div class="showcase-text"><h3>Clickable terminals</h3><p>Members, message IDs and IFS paths in any terminal open or explain themselves.</p><p><a href="{{ "/features-3-1.html" | relative_url }}">Read more →</a></p></div><div class="showcase-demo"><div class="demo"><div class="demo-bar"><span class="dots"><i></i><i></i><i></i></span><span class="file">Terminal</span><span class="label">Ctrl+click to open or explain</span></div><pre class="demo-code"><span class="line">&gt; CRTBNDRPG PGM(APPLIB/ORDERS) SRCFILE(<span class="sel">APPLIB/QRPGLESRC(ORDERS)</span>)</span><span class="line">  <span class="sel">RNF7030</span> The name or indicator CUSTNAM is not defined.</span><span class="line">  See <span class="sel">/home/dev/build/orders.log</span> for details.</span></pre></div></div></div>
