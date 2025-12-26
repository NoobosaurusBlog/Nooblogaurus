---
layout: default
title: cshake
short_title: cshake
summary: TLS handshake analyzer with OCSP/CRL checks, Rich dashboards, and exportable JSON/YAML/HTML outputs.
---

<div class="panel">
<h1>cshake</h1>
<p>A minimal-yet-practical TLS handshake inspection CLI. Combines curl stage tracing, PyOpenSSL certificate pulls, ephemeral key detection, and dual revocation checks. Think of it as an interactive microscope rather than a heavyweight scanner.</p>
</div>

<div class="panel">
<h2>// Feature Highlights</h2>
<ul>
  <li>Single-shot or real-time (<code>-r</code>) curl tracing with Rich tables/animations.</li>
  <li>Certificate chain parsing, weak cipher warnings, CN/SAN validation, expiry alerts.</li>
  <li>OCSP + CRL lookups for revocation intel.</li>
  <li>Ephemeral key detection (ECDHE, DHE, X25519).</li>
  <li>Structured exports: <code>--output-format json|yaml|html</code> via <code>cshake.output</code>.</li>
  <li>Bulk support with <code>--input-file</code>.</li>
</ul>
</div>

<div class="panel">
<h2>// Quick Start</h2>
<pre><code>cd cshake
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python3 cshake.py https://example.com
python3 cshake.py -r -v https://example.com --output-format html -o report.html
python3 cshake.py --input-file urls.txt --tlsv 1.2 --output-format json</code></pre>
</div>

<div class="panel">
<h2>// Display Modes</h2>
<p>The Rich UI mixes summary panels, chain tables, per-stage status, and optional ASCII animation (<code>--ascii</code>). HTML/JSON/YAML renders come from <code>cshake/output.py</code> and a Jinja template (<code>report_template.html</code>). Screenshots live under <code>cshake/screenshots/</code>.</p>
</div>

<div class="panel">
<h2>// Notes & Limitations</h2>
<ul>
  <li>Does not call <code>get_verify_result()</code>, so trust is reported as “Unknown”.</li>
  <li>OCSP responses depend on responder behavior; CRL queries require distribution points.</li>
  <li>IPv6 support is minimal right now.</li>
  <li>Processes one host at a time (extend <code>process_urls</code> for concurrency).</li>
</ul>
<a class="button" href="https://github.com/noobosaurus-r3x/cshake">GitHub Repo</a>
</div>

<div class="panel">
<h2>// Full README</h2>
{% capture readme %}
{% include readmes/cshake.md %}
{% endcapture %}
{{ readme | markdownify }}
</div>
