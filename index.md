---
title: Welcome
layout: default
permalink: /
---

<div class="panel">
<h1>&gt; Booting Blogosaurus...</h1>
<p>This showroom stitches together my operators' toolkit: TLS inspection, DNS reconnaissance, OSINT automation, Tor metadata scraping, session cookie tinkering, red-flag harvesting, and a whole crate of cheat sheets.</p>
<p>Pick a system, read the docs, grab the code, and keep shipping.</p>
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
<p>Need quick syntax reminders? The <a href="{{ '/resources/' | relative_url }}">Cheat Sheets safe</a> mirrors my personal crib notes for tools like nmap, Hydra, Hashcat, ffuf, Docker, SMB utilities, and Tshark.</p>
<a class="button" href="{{ '/resources/' | relative_url }}">Browse Cheat Sheets</a>
</div>

<div class="panel">
<h2>// Deployment Notes</h2>
<ul>
<li>GitHub Pages-ready Jekyll site. Point Pages to <code>Blogosaurus/</code> and the grids light up.</li>
<li>Install deps via <code>bundle install</code>; serve locally with <code>bundle exec jekyll serve --livereload</code>.</li>
<li>Theme aims for phosphor monitors: neon text, dashed borders, blinking prompt. Hack away if you prefer different vibes.</li>
</ul>
</div>
