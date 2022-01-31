---
title: "wecode 문제풀이" #사이드바 클릭시 메인으로 들어가서 보이는 제목
layout: archive
permalink: categories/wecode #_pages > categories 파일이름으로 설정
author_profile: true #9번 라인의 변수와, includes > nav_list_main의 post.md를 지정하는 변수가 같아야함
sidebar_main: true
---

{% assign posts = site.categories.Wecode %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
