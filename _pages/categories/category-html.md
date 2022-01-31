---
title: "HTML"
layout: archive
permalink: categories/html #9번 라인의 이름과 통일시켜야함 -> nav_list_main 수정해야함
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.HTML %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
