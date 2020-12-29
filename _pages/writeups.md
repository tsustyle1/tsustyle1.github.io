---
title: "Writeups"
permalink: /writeups/
---

<ul>
{% for post in posts %}
  {% if post.tags contains "htb" %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <span class="date">{{ post.date | date: "%B %-d, %Y"  }}</span>
  </li>
  {% endif %}
{% endfor %}
</ul>
