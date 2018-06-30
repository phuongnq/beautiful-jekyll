---
layout: page
title: 記事
subtitle: 日本語記事一覧
permalink: category/japanese/index.html
---

<ul>
    {% for post in site.posts %}
        {% if post.categories contains 'japanese' %}
            <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
        {% endif %}
    {% endfor %}
</ul>