---
title: Welcome
layout: default
permalink: /
---

<div class="panel">
<h1>&gt; Booting Nooblogosaurus...</h1>
<p>Just parking the tools and notes I'm tinkering with so they're easy to find (for me and anyone else who needs them). Nothing flashy. Each link points straight to source, docs, and examples.</p>
<p>If something helps you, awesome. If not, that’s cool too.</p>
</div>

<div class="panel">
<h2>// Toolchain</h2>
<div class="tool-grid">
{% assign cards = site.tools | sort: 'title' %}
{% for tool in cards %}
  <a class="tool-card" href="{{ tool.url | relative_url }}">
    <h3>{{ tool.title }}</h3>
    <p>{{ tool.summary }}</p>
  </a>
{% endfor %}
</div>
</div>

<div class="panel">
<h2>// Resources</h2>
<p>Need a reminder mid-engagement? The <a href="{{ '/resources/' | relative_url }}">cheat-sheet shelf</a> mirrors my scratchpad pages for nmap, Hydra, Hashcat, ffuf, Docker, SMB utilities, Tshark, and more.</p>
<a class="button" href="{{ '/resources/' | relative_url }}">Browse Cheat Sheets</a>
</div>
