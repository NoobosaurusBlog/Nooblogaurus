---
title: Tools
permalink: /tools/
layout: default
---

<div class="panel">
<h1>// Tools</h1>
<p>Everything in one place. These are the utilities currently bundled with Nooblogaurus.</p>
</div>

<div class="panel">
<div class="tool-grid">
{% assign sorted_tools = site.tools | sort: 'title' %}
{% for tool in sorted_tools %}
  <a class="tool-card" href="{{ tool.url | relative_url }}">
    <h3>{{ tool.title }}</h3>
    <p>{{ tool.summary }}</p>
  </a>
{% endfor %}
</div>
</div>
