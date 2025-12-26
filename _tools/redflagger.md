---
layout: default
title: RedFlagger
short_title: RedFlagger
summary: Bash script that mirrors red.flag.domains daily feeds with flexible date selectors.
---

<div class="panel">
<h1>RedFlagger</h1>
<p>Simple bash helper for <code>https://dl.red.flag.domains/daily/</code>. Fetch latest or historical feeds, concatenate them, and keep the output sorted—great for threat intel baselines.</p>
</div>

<div class="panel">
<h2>// Usage</h2>
<pre><code>cd redflagger
chmod +x redflagger.sh
./redflagger.sh -l -o latest.txt       # yesterday's file
./redflagger.sh -d 3 -o sample.txt     # 3 days ago
./redflagger.sh -a -o everything.txt   # pull them all
./redflagger.sh -d 7 -a -o window.txt  # since 7 days ago, then all others</code></pre>
<p>Options:</p>
<ul>
  <li><code>-l</code>/<code>--latest</code> – 1 day ago.</li>
  <li><code>-d &lt;num&gt;</code>/<code>--days</code> – Pick <em>n</em> days ago.</li>
  <li><code>-a</code>/<code>--all</code> – Download every listed archive.</li>
  <li><code>-o &lt;file&gt;</code> – Output destination (default: <code>output.txt</code>).</li>
</ul>
</div>

<div class="panel">
<h2>// Implementation</h2>
<ul>
  <li>Fetches the directory listing, scrapes YYYY-MM-DD entries, and deduplicates downloads.</li>
  <li>Each file is appended to the chosen output, then the file is sorted.</li>
  <li><code>set -euo pipefail</code> + helpful error messages keep it predictable.</li>
</ul>
<a class="button" href="https://github.com/noobosaurus-r3x/NewRedflag" target="_blank">Original Inspiration</a>
</div>

<div class="panel">
<h2>// Full README</h2>
{% capture readme %}
{% include readmes/redflagger.md %}
{% endcapture %}
{{ readme | markdownify }}
</div>
