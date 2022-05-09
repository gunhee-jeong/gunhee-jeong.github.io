---
title: "코딩 테스트" #사이드바를 눌러서 들어가면 보이는 제목
layout: archive
permalink: categories/codingTest
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.codingTest %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
