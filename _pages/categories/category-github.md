---
title: "Github" #왼쪽 사이드바에 나타나는 글씨
layout: archive
permalink: categories/github #9번 라인에도 변수 있음 -> nav_list_main 수정해야함
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.Github %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
