---
layout: page
title: Portfolio
permalink: /portfolio
---

{% for item in site.portfolio %}
## [{{ item.title }}]({{ item.url | relative_url }})
{{ item.description }}
{% endfor %}
