---
layout: page
title: Nhật Bản
subtitle: Bài viết liên quan Nhật Bản và cuộc sống bên Nhật Bản
---

<ul>
    {% for post in site.posts %}
        {% if post.categories contains 'japan-life' %}
            <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
        {% endif %}
    {% endfor %}
</ul>