---
layout: page
title: Programming
subtitle: List of posts about programming
permalink: category/programming
---

<ul>
    {% for post in site.posts %}
        {% if post.categories contains 'programming' %}
            <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
        {% endif %}
    {% endfor %}
</ul>