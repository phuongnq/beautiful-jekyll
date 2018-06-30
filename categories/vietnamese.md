---
layout: page
title: Bài viết
subtitle: Danh sách bài viết tiếng Việt
permalink: category/vietnamese/index.html
---

<ul>
    {% for post in site.posts %}
        {% if post.categories contains 'vietnamese' %}
            <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
        {% endif %}
    {% endfor %}
</ul>