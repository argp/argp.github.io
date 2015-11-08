---
layout: default
title: archive
---

{% for post in site.posts %}
    <li>
        <a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
        <small>{{ post.date | date_to_string }}</small>
    </li>
{% endfor %}
