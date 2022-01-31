---
title: "프로그래머스 문제 풀이"
layout: archive
permalink: categories/programmers #9번 라인의 이름과 통일시켜야함 -> nav_list_main 수정해야함
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.programmers %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
