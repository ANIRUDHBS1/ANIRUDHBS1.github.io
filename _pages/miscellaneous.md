---
layout: archive
title: "misc"
permalink: /miscellaneous/
author_profile: true
---

{% include base_path %}

{% for post in site.misc reversed %}
  {{ post.content }}
{% endfor %}
