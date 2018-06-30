---
layout: page
title: Job Information
subtitle: List of jobs
permalink: category/job
---


<ul>
    {% for post in site.posts %}
        {% if post.categories contains 'job' %}
            <li><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></li>
        {% endif %}
    {% endfor %}
</ul>