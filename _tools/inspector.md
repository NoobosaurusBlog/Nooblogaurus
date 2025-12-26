---
layout: default
title: InspecTor
short_title: InspecTor
summary: Tor-aware metadata crawler for onion+clearnet targets with JSON/SQLite/HR output.
---

<div class="panel">
<h1>InspecTor</h1>
<p>Scrape metadata from onion services or regular sites while tunneling through Tor. Supports concurrent requests, Selenium fallbacks, JSON/stdout/SQLite outputs, and optional human-readable dumps.</p>
</div>

<div class="panel">
<h2>// Capabilities</h2>
<ul>
  <li>Accepts URLs via <code>-u</code> or file list (<code>-f</code>). Forces Tor routing with <code>--force-tor</code>.</li>
  <li>Extract and filter fields (<code>--fields</code> or <code>--extract-all</code>): headers, links, crypto wallets, phone numbers, assets, etc.</li>
  <li>Concurrent ThreadPool workers with retry-aware requests sessions.</li>
  <li>Optional Selenium (ChromeDriver) capture for JS-heavy sites.</li>
  <li>Persistence: JSON file, stdout (<code>-o -</code>), and SQLite (<code>--database</code>).</li>
  <li>Colored human-readable output via <code>colorama</code>.</li>
</ul>
</div>

<div class="panel">
<h2>// Runbook</h2>
<pre><code>cd InspecTor
pip install -r requirements.txt
python3 InspecTor.py -u https://exampleonionsite.onion --extract-all -o all.json --human-readable
python3 InspecTor.py -f urls.txt --fields emails phone_numbers links --default-region FR --force-tor
python3 InspecTor.py -u https://example.com --use-selenium --no-verify-ssl
</code></pre>
<p>Make sure the Tor SOCKS proxy is reachable at <code>127.0.0.1:9050</code> when scraping onions or forcing Tor.</p>
</div>

<div class="panel">
<h2>// Architecture</h2>
<ul>
  <li><code>setup_session()</code> wires Tor proxies + retry adapters.</li>
  <li><code>extract_metadata()</code> orchestrates soup parsing, heuristics for wallets, regex-based selectors, and optional Selenium fallback.</li>
  <li><code>save_to_database()</code> stores normalized JSON fragments per URL.</li>
  <li>Phone numbers pass through <code>phonenumbers</code> with region override.</li>
</ul>
<a class="button" href="https://github.com/noobosaurus-r3x/InspecTor">GitHub Repo</a>
</div>

<div class="panel">
<h2>// Full README</h2>
{% capture readme %}
{% include readmes/inspector.md %}
{% endcapture %}
{{ readme | markdownify }}
</div>
