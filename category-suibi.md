---
layout: page
title: 随笔
permalink: /category/随笔/
---

{% assign posts = site.categories["随笔"] %}
{% assign posts_by_year = posts | group_by_exp: "post", "post.date | date: '%Y'" %}
{% for year in posts_by_year %}
<h3 class="year-label">{{ year.name }}</h3>
<ul class="archive">
{% for post in year.items %}
  <li><time>{{ post.date | date: "%m-%d" }}</time><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></li>
{% endfor %}
</ul>
{% endfor %}
