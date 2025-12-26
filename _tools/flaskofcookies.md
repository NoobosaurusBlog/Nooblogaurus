---
layout: default
title: Flask Of Cookies
short_title: FlaskOfCookies
summary: Encode/decode Flask session cookies or brute-force the secret key with a wordlist.
---

<div class="panel">
<h1>Flask Of Cookies</h1>
<p>A tiny CLI inspired by <em>flask-session-cookie-manager</em> that lets you encode, decode, or brute-force Flask session cookies. Handy for CTFs or verifying secret key hygiene.</p>
</div>

<div class="panel">
<h2>// Modes</h2>
<ul>
  <li><strong>encode</strong> – Convert a Python dict string into a signed cookie using your secret key.</li>
  <li><strong>decode</strong> – Pull the payload with or without the secret key.</li>
  <li><strong>bruteforce</strong> – Iterate wordlists until the serializer loads successfully.</li>
</ul>
</div>

<div class="panel">
<h2>// Usage</h2>
<pre><code>cd FlaskOfCookies
python3 FOC.py encode -s 'secret' -t "{'user':'admin'}"
python3 FOC.py decode -c &lt;cookie&gt;
python3 FOC.py decode -s 'secret' -c &lt;cookie&gt;
python3 FOC.py bruteforce -c &lt;cookie&gt; -w /path/to/wordlist.txt
</code></pre>
<p>Under the hood, <code>itsdangerous.URLSafeTimedSerializer</code> plus Flask’s default salt (<code>cookie-session</code>) handle signing. <code>brute_force()</code> prints live attempts with a CLI progress effect.</p>
</div>

<div class="panel">
<h2>// Notes</h2>
<ul>
  <li>Input structures are evaluated with <code>ast.literal_eval</code>; keep them valid dict strings.</li>
  <li><code>decode()</code> gracefully handles secret-less payload inspection by manually base64 decoding.</li>
  <li>Wordlist attack stops on first valid signature and announces the key.</li>
</ul>
<a class="button" href="https://github.com/noobosaurus-r3x/FlaskOfCookies">GitHub Repo</a>
</div>

<div class="panel">
<h2>// Full README</h2>
{% capture readme %}
{% include readmes/flaskofcookies.md %}
{% endcapture %}
{{ readme | markdownify }}
</div>
