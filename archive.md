---
layout: page
title: archive
---

{% for post in site.posts %}
  <sup><sub>{{ post.date | date_to_string }}</sub></sup> [ {{ post.title }} ]({{ post.url }})
{% endfor %}
