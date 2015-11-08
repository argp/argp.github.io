---
layout: page
title: archive
---

{% for post in site.posts %}
<small>
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }})
</small>
{% endfor %}
