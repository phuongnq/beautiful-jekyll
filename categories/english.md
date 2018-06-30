---
layout: page
title: Posts
subtitle: List of post in English
permalink: category/english/index.html
---

<ul>
    {% for post in site.posts %}
        {% if post.categories contains 'english' %}
            <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
        {% endif %}
    {% endfor %}
</ul>