---
layout: notag
title: Category - Github Trending
---
<br/>
{% for p in site.posts %}
{% for t in p.category %}
{% if t == "Tutorial" %}
<a class="list-group-item" href="{{p.url}}">
	{{p.date | date: "%b %d, %Y"}} - {{p.title}}
</a>
{% endif %}
{% endfor %}
{% endfor %}