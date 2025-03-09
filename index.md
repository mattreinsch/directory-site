---
layout: default
title: AI Tools Directory
---

<h1>AI Tools Directory</h1>

<ul>
  {% for tool in site.data.tools %}
    <li>
      <strong>{{ tool.name }}</strong> - {{ tool.category }} 
      (<a href="{{ tool.website }}">Website</a>)
    </li>
  {% endfor %}
</ul>
