---
layout: default
title: "Db2 for i & data"
parent: "Features"
nav_order: 3
has_children: true
has_toc: false
---

# Db2 for i & data

Query, edit, compare, import and export the data in Db2 for i.
{: .fs-6 .fw-300 }

![SQL scripts are checked before you run them.]({{ "/images/sql-checks.png" | relative_url }})
*SQL scripts are checked before you run them.*

| Page | What you get |
|---|---|
| [SQL & table data](features-sql-data.md) | Db2 for i SQL with autocomplete and table data edited in a safe grid. |
| [SQL power tools](features-sql-tools.md) | Generate DDL, run whole scripts, Explain, SQL history and saved queries. |
| [Insights](features-insights.md) | Index advisor, DEV ↔ PROD data compare, message help on hover, job log analyzer. |
| [Data, performance & quality](features-data-quality.md) | Excel / CSV / JSON import and export, performance monitor, code metrics, RPGUnit tests. |
| [Index Advice Chart](features-3-2.md#index-advice-chart) *(3.2)* | The indexes Db2 asked for, merged and ranked, with the CREATE INDEX for each. |

## Examples

<div class="showcase"><div class="showcase-text"><h3>SQL checks before you run</h3><p>Risky statements are flagged in every SQL script; <strong>Add WHERE 1 = 1</strong> says that every row is really meant.</p><p><a href="{{ "/features-sql-data.html" | relative_url }}">Read more →</a></p></div><div class="showcase-demo"><div class="demo"><div class="demo-bar"><span class="dots"><i></i><i></i><i></i></span><span class="file">cleanup.sql</span></div><pre class="demo-code"><span class="line"><span class="c">-- Monthly clean-up</span></span><span class="line"><span class="warn"><span class="k">DELETE</span></span> <span class="k">FROM</span> ORDERS;</span><span class="line"><span class="k">UPDATE</span> CUSTOMER <span class="k">SET</span> REGION = <span class="s">'EU'</span> <span class="k">WHERE</span> COUNTRY <span class="warn">= <span class="k">NULL</span></span>;</span><span class="line"><span class="info"><span class="k">DROP</span></span> <span class="k">TABLE</span> OLD_ORDERS;</span></pre><div class="demo-problems"><div class="demo-problems-title">Problems</div><div class="demo-msg"><span class="ico w">!</span><span class="t">DELETE without WHERE changes every row of the table. Add a WHERE (or WHERE 1 = 1 if that is really what you want).</span><span class="r">sql-without-where</span></div><div class="demo-msg"><span class="ico w">!</span><span class="t">= NULL is never true: use IS NULL.</span><span class="r">sql-equals-null</span></div><div class="demo-msg"><span class="ico i">i</span><span class="t">This statement cannot be undone: check the system and the library first (and keep a copy of the data).</span><span class="r">sql-irreversible</span></div></div></div></div></div>
