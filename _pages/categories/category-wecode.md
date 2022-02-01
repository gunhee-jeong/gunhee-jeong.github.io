---
title: "위코드 문제 풀이"
layout: archive
permalink: categories/wecode #9번 라인에도 변수 있음 -> nav_list_main 수정해야함
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Wecode %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
