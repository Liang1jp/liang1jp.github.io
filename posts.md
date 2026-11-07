---
layout: page
title: 文章
permalink: /posts/
---

<style>
.cat-nav { list-style: none; padding: 0; margin: 0 0 2.2em; display: flex; flex-wrap: wrap; gap: 8px; }
.cat-nav button { font: inherit; cursor: pointer; background: none; display: inline-flex; gap: 6px; align-items: baseline; padding: 3px 12px; border: 1px solid #ddd; border-radius: 999px; font-size: .85em; color: #666; }
.cat-nav button:hover { border-color: #999; color: #111; }
.cat-nav button.active { border-color: #333; color: #111; background: #f4f4f2; }
.cat-nav button em { font-style: normal; color: #aaa; font-size: .9em; }
.year-label { font-size: .8em; font-weight: normal; letter-spacing: .08em; color: #aaa; margin: 2em 0 .5em; padding-bottom: 6px; border-bottom: 1px solid #eee; }
.archive { list-style: none; padding: 0; margin: 0 0 1em; }
.archive li { display: flex; gap: 16px; padding: 5px 0; line-height: 1.6; }
.archive time { color: #bbb; font-variant-numeric: tabular-nums; flex: 0 0 3.2em; font-size: .9em; }
.archive a { text-decoration: none; color: #333; }
.archive a:hover { text-decoration: underline; }
</style>

<ul class="cat-nav">
  <li><button type="button" data-filter="all" class="active">全部 <em>{{ site.posts.size }}</em></button></li>
{% for category in site.categories %}
  <li><button type="button" data-filter="{{ category[0] }}">{{ category[0] }} <em>{{ category[1].size }}</em></button></li>
{% endfor %}
</ul>

{% assign posts_by_year = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
{% for year in posts_by_year %}
<h3 class="year-label">{{ year.name }}</h3>
<ul class="archive">
{% for post in year.items %}
  <li data-cat="{{ post.categories | join: ' ' }}"><time>{{ post.date | date: "%m-%d" }}</time><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></li>
{% endfor %}
</ul>
{% endfor %}

<script>
(function(){
  var btns = document.querySelectorAll('.cat-nav button');
  var lists = document.querySelectorAll('.archive');
  btns.forEach(function(btn){
    btn.addEventListener('click', function(){
      var cat = btn.getAttribute('data-filter');
      btns.forEach(function(b){ b.classList.remove('active'); });
      btn.classList.add('active');
      document.querySelectorAll('.archive li').forEach(function(li){
        var cats = (li.getAttribute('data-cat') || '').split(/\s+/).filter(Boolean);
        li.style.display = (cat === 'all' || cats.indexOf(cat) !== -1) ? '' : 'none';
      });
      lists.forEach(function(ul){
        var visible = false;
        ul.querySelectorAll('li').forEach(function(li){ if (li.style.display !== 'none') visible = true; });
        ul.style.display = visible ? '' : 'none';
        var h = ul.previousElementSibling;
        if (h && h.classList.contains('year-label')) h.style.display = visible ? '' : 'none';
      });
    });
  });
})();
</script>
{% endfor %}
</ul>
{% endfor %}
{% endfor %}
