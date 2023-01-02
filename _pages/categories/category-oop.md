---
title: "객체 지향의 사실과 오해"
layout: archive
permalink: categories/oop
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['OOP'] %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
