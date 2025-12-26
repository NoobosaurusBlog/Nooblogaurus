---
layout: default
title: DNSpector
short_title: DNSpector
summary: dig + whois automation with colorized output, passive subdomain scraping, and AXFR testing.
---

<div class="panel">
<h1>DNSpector</h1>
<p>A helper that wraps <code>dig</code>, <code>whois</code>, and passive subdomain APIs for fast DNS situational awareness. No reinvention—just automation plus tidy output.</p>
</div>

<div class="panel">
<h2>// Capabilities</h2>
<ul>
  <li>Query chosen record types or <code>-r all</code> (A/AAAA/CNAME/MX/NS/etc.).</li>
  <li>WHOIS summaries with missing-field handling (<code>whois_module.py</code>).</li>
  <li>Passive subdomain grabs from RapidDNS, crt.sh, OTX, urlscan, and the Wayback Machine.</li>
  <li>Zone transfer checks via <code>dns.query.xfr</code>.</li>
  <li>Color coding + friendly “no records found” messaging.</li>
</ul>
</div>

<div class="panel">
<h2>// Usage</h2>
<pre><code>cd DNSpector
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python3 DNSpector.py example.com -r A MX -w
python3 DNSpector.py example.com -r all -sd -zt
python3 DNSpector.py example.com -n 1.1.1.1 -r TXT SPF</code></pre>
<p>By default DNSpector uses the resolver’s first nameserver. <code>-n</code> overrides it.</p>
</div>

<div class="panel">
<h2>// Implementation Notes</h2>
<ul>
  <li><code>dns_module.py</code> normalizes record lists, runs <code>dig</code>, and trims comments.</li>
  <li><code>subdomain_module.py</code> fans out concurrent HTTP fetches and merges matches.</li>
  <li><code>utils.py</code> centralizes ANSI colors + subprocess timeout handling.</li>
</ul>
<a class="button" href="https://github.com/noobosaurus-r3x/DNSpector">GitHub Repo</a>
</div>

<div class="panel">
<h2>// Full README</h2>
{% capture readme %}
{% include readmes/dnspector.md %}
{% endcapture %}
{{ readme | markdownify }}
</div>
