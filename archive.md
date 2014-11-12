---
layout: page
title: Archive
---

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &raquo; [ {{ post.title }} ]({{ post.url }}) {% if post.tags.size > 0 %}{% include tag-list.html %} {% endif %}
{% endfor %}

