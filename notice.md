---
layout: notag
title: 공지사항
---

KCBS 블로그의 공지사항들입니다.

<div class="list-group">
<a class="list-group-item active" href="#">공지사항</a>
{% for p in site.posts %}
{% if p.category == "notice" %}
<a class="list-group-item" href="{{p.url}}">[{{p.date | date: "%B %d, %Y"}}] {{p.title}}</a>
{% endif %}
{% endfor %}
</div>