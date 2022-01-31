---
title: "blog" #왼쪽 사이드바에 나타나는 글씨
layout: archive
permalink: categories/blog #9번 라인의 이름과 통일시켜야함 -> nav_list_main 수정해야함
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Blog %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
