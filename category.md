---
layout: page
title: Categories
subtitle: Posts by categories
---

**Browse post by following categories:**

<ul>
    {% for category in site.categories %}
        <li><a href="{{ site.url }}/category/{{ category | first | url_encode }}/">{{ category | first }}</a></li>
    {% endfor %}
</ul>