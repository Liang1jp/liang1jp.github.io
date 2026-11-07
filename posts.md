---
layout: page
title: 文章
permalink: /posts/
---

<style>
.cat-nav { list-style: none; padding: 0; margin: 0 0 2.2em; display: flex; flex-wrap: wrap; gap: 8px; }
.cat-nav a { display: inline-flex; gap: 6px; align-items: baseline; padding: 3px 12px; border: 1px solid #ddd; border-radius: 999px; font-size: .85em; text-decoration: none; color: #666; }
.cat-nav a:hover { border-color: #999; color: #111; }
.cat-nav a em { font-style: normal; color: #aaa; font-size: .9em; }
.year-label { font-size: .8em; font-weight: normal; letter-spacing: .08em; color: #aaa; margin: 2em 0 .5em; padding-bottom: 6px; border-bottom: 1px solid #eee; }
.archive { list-style: none; padding: 0; margin: 0 0 1em; }
.archive li { display: flex; gap: 16px; padding: 5px 0; line-height: 1.6; }
.archive time { color: #bbb; font-variant-numeric: tabular-nums; flex: 0 0 3.2em; font-size: .9em; }
.archive a { text-decoration: none; color: #333; }
.archive a:hover { text-decoration: underline; }
</style>

<ul class="cat-nav">
{% for category in site.categories %}
  <li><a href="#cat-{{ category[0] }}">{{ category[0] }} <em>{{ category[1].size }}</em></a></li>
{% endfor %}
  <li><a href="#all">全部 <em>{{ site.posts.size }}</em></a></li>
</ul>

<h2 id="all">全部</h2>
{% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
{% for year in posts_by_year %}
<h3 class="year-label">{{ year.name }}</h3>
<ul class="archive">
{% for post in year.items %}
  <li><time>{{ post.date | date: "%m-%d" }}</time><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></li>
{% endfor %}
</ul>
{% endfor %}

{% for category in site.categories %}
<h2 id="cat-{{ category[0] }}">{{ category[0] }}</h2>
{% assign cat_by_year = category[1] | group_by_exp: "post", "post.date | date: '%Y'" %}
{% for year in cat_by_year %}
<h3 class="year-label">{{ year.name }}</h3>
<ul class="archive">
{% for post in year.items %}
  <li><time>{{ post.date | date: "%m-%d" }}</time><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></li>
{% endfor %}
</ul>
{% endfor %}
{% endfor %}
