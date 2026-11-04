---
layout: home
title: Home
nav_order: 1
permalink: /
description: "Vanthrex for IBM i — connect, browse, edit, compile, query and monitor IBM i from VS Code."
---

<div class="hero">
  <h1>Vanthrex for IBM i</h1>
  <p>One sidebar for everything you do on IBM i: connect, browse, edit, compile, query, monitor and fix — with checks while you type, an AI assistant, Git and a call graph built in. In VS Code, without a green screen.</p>
  <a class="btn btn-primary fs-5" href="https://marketplace.visualstudio.com/items?itemName=gauravgupta0612.vanthrex-ibmi">Install from the Marketplace</a>
  <a class="btn btn-outline fs-5" href="{{ "/installation.html" | relative_url }}">Get started</a>
  <a class="btn btn-outline fs-5" href="{{ "/screenshots.html" | relative_url }}">See screenshots</a>
  <div class="badges"><span>Version 3.0.0</span><span>Free · MIT License</span><span>RPG · CL · SQL · DDS · COBOL</span><span>8 languages</span></div>
</div>

![Vanthrex in VS Code: RPG checks while you type]({{ "/images/rpg-checks.png" | relative_url }})
*Checks while you type in RPG, CL and SQL, with the fix one click away.*

## What you can do

<div class="cards">
  <a class="card" href="{{ "/features-explore.html" | relative_url }}"><span class="card-icon">🔌</span><span class="card-title">Connect & explore</span><span class="card-text">Several systems at once, libraries, objects, the IFS, PDM in one screen and the System Tracker.</span></a>
  <a class="card" href="{{ "/features-develop.html" | relative_url }}"><span class="card-icon">✍️</span><span class="card-title">Develop</span><span class="card-text">SEU source dates and F4, Ctrl+Alt+C compile, 50+ checks with quick fixes, call graph, Git, debug and AI.</span></a>
  <a class="card" href="{{ "/features-data.html" | relative_url }}"><span class="card-icon">🗄️</span><span class="card-title">Db2 for i & data</span><span class="card-text">SQL with autocomplete, a safe data grid, Explain, index advisor, DEV ↔ PROD compare, Excel / CSV / JSON.</span></a>
  <a class="card" href="{{ "/features-operate.html" | relative_url }}"><span class="card-icon">⚙️</span><span class="card-title">Operate the system</span><span class="card-text">Jobs, QSYSOPR, spooled files, subsystems, user profiles, journals, authorities, storage — production-safe.</span></a>
  <a class="card" href="{{ "/coming-from-code-for-ibmi.html" | relative_url }}"><span class="card-icon">👥</span><span class="card-title">Work as a team</span><span class="card-text">Import from Code for IBM i, one team setup file, shared coding standards and a code health report.</span></a>
  <a class="card" href="{{ "/features-3-0.html" | relative_url }}"><span class="card-icon">🆕</span><span class="card-title">What's new in 3.0</span><span class="card-text">AS/400 GO menus, team setup, team coding standards and the code health report of whole libraries.</span></a>
</div>

## See it in action

<div class="shot-grid">
  <figure><a href="{{ "/screenshots.html" | relative_url }}"><img src="{{ "/images/quick-fix.png" | relative_url }}" alt="Quick fix after CHAIN" loading="lazy"></a><figcaption>Quick fix after CHAIN</figcaption></figure>
  <figure><a href="{{ "/screenshots.html" | relative_url }}"><img src="{{ "/images/suggestions.png" | relative_url }}" alt="Suggestions while you type" loading="lazy"></a><figcaption>Suggestions while you type</figcaption></figure>
  <figure><a href="{{ "/screenshots.html" | relative_url }}"><img src="{{ "/images/fixed-to-free-compare.png" | relative_url }}" alt="Fixed → free in one command" loading="lazy"></a><figcaption>Fixed → free in one command</figcaption></figure>
  <figure><a href="{{ "/screenshots.html" | relative_url }}"><img src="{{ "/images/flowchart.png" | relative_url }}" alt="Flowchart of a procedure" loading="lazy"></a><figcaption>Flowchart of a procedure</figcaption></figure>
  <figure><a href="{{ "/screenshots.html" | relative_url }}"><img src="{{ "/images/developer-toolbox.png" | relative_url }}" alt="Developer Toolbox (Ctrl+Alt+A)" loading="lazy"></a><figcaption>Developer Toolbox (Ctrl+Alt+A)</figcaption></figure>
  <figure><a href="{{ "/screenshots.html" | relative_url }}"><img src="{{ "/images/team-standards.png" | relative_url }}" alt="Team coding standards" loading="lazy"></a><figcaption>Team coding standards</figcaption></figure>
</div>

[All screenshots]({{ "/screenshots.html" | relative_url }}){: .btn }

## Start in five minutes

<ol class="steps">
  <li><a href="{{ "/installation.html" | relative_url }}"><strong>Install the extension</strong></a> from the Marketplace, or run <code>code --install-extension gauravgupta0612.vanthrex-ibmi</code>.</li>
  <li><a href="{{ "/ibm-i-setup.html" | relative_url }}"><strong>Check the IBM i</strong></a>: usually only the SSH server is needed (<code>STRTCPSVR SERVER(*SSHD)</code>).</li>
  <li><a href="{{ "/first-connection.html" | relative_url }}"><strong>Create your first connection</strong></a> with the guided form and <em>Test connection</em>.</li>
  <li>Coming from Code for IBM i? <a href="{{ "/coming-from-code-for-ibmi.html" | relative_url }}"><strong>Import your setup</strong></a> in one step.</li>
  <li>Press <kbd>Ctrl+Alt+A</kbd> in any source to see every tool that fits it, and learn the <a href="{{ "/keyboard-shortcuts.html" | relative_url }}">keyboard shortcuts</a>.</li>
</ol>

Something not working? See [Troubleshooting](troubleshooting.md) and the [FAQ](faq.md).

---

Current version: **3.0.0** · [What's new](whats-new.md) · [Changelog](changelog.md) · Free and open source under the MIT License.
