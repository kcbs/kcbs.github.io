---
layout: notag
title: Category - 
---
{% for p in site.posts %}
	{% for t in p.category %}
		{% if t ==  %}
			<a class="list-group-item" href="{{p.url}}">{{p.title}}</a>
		{% endif %}
	{% endfor %}
{% endfor %}