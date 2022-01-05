---
title: "HTML/CSS/JavaScript"
layout: archive
permalink: categories/web
author_profile: true
sidebar_main: true
---


{% assign posts = site.categories.codding_everybody %}
{% for post in posts %} {% include archive-single2.html type=page.entries_layout %} {% endfor %}
