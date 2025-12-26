---
layout: default
title: Navarro
short_title: Navarro
summary: Username OSINT checker covering 25+ platforms with smart rate limiting and Rich dashboards.
---

<div class="panel">
<h1>Navarro</h1>
<p>OSINT username sweeper that hits 25+ social services without API keys. Handles rate limiting, rotates user agents, pools sessions, and renders results via Rich tables or plain text.</p>
</div>

<div class="panel">
<h2>// Highlights</h2>
<ul>
  <li>Per-platform logic with status categories: found, not found, rate limited, timeout, network, unknown.</li>
  <li>Persistent adaptive delays saved to <code>~/.navarro_rate_limits.json</code>.</li>
  <li>Session pool with UA rotation to minimize fingerprints.</li>
  <li>Progress bars + tables when Rich is installed.</li>
  <li>JSON export bundling stats + found profile URLs.</li>
  <li>Batch input via <code>--list</code> or single username argument.</li>
</ul>
</div>

<div class="panel">
<h2>// Usage</h2>
<pre><code>cd Navarro
pip install -r requirements.txt
python3 navarro.py noobosaurus
python3 navarro.py --list handles.txt --export results.json
python3 navarro.py hacker --export matches.json</code></pre>
<p>After each username, the CLI prints summary stats plus Rich/ASCII tables. Export format mirrors the README example for easy downstream parsing.</p>
</div>

<div class="panel">
<h2>// Platform Coverage</h2>
<p>GitHub, GitLab, Reddit, Instagram, Facebook, TikTok, LinkedIn, Pinterest, Pastebin, Telegram, Snapchat, Strava, Threads, Mastodon, Bluesky, Spotify, SoundCloud, YouTube, Medium, Chess.com, Keybase, Linktree, VK, Steam, DeviantArt, Vimeo. (X/Twitter and Twitch intentionally excluded.)</p>
<a class="button" href="https://github.com/noobosaurus-r3x/Navarro">GitHub Repo</a>
</div>

<div class="panel">
<h2>// Full README</h2>
{% capture readme %}
{% include readmes/navarro.md %}
{% endcapture %}
{{ readme | markdownify }}
</div>
