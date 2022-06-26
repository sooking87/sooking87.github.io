---
title: "피그마 입문"
layout: archive
permalink: categories/figma
author_profile: true
sidebar_main: true
---

{% assign posts = site.categories['Figma'] %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
