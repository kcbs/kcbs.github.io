---
layout: notag
title: 공지사항
---

KCBS 블로그의 공지사항들입니다.

{% for p in site.posts %}
{% if p.category == "notice" %}
* <a href="{{p.url}}">[{{p.date | date: "%B %d, %Y"}}] {{p.title}}</a>
{% endif %}
{% endfor %}