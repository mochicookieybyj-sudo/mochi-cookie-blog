---
layout: default
title: Home
---

# Mochi Cookie Blog

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | relative_url }}) - {{ post.date | date: "%Y-%m-%d" }}
{% else %}
No posts yet.
{% endfor %}
