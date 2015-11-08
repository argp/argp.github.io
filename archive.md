---
layout: page
title: archive
---

{% for post in site.posts %}
  * [ {{ post.title }} ]({{ post.url }}) <sup><sub>{{ post.date | date_to_string }}</sub></sup>
{% endfor %}
