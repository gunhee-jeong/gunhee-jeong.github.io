---
title: "wecode" #사이드바를 눌러서 들어가면 보이는 제목
layout: archive
permalink: categories/wecodes
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories.wecodes %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
