---
title: "DataStructures"
layout: archive
permalink: categories/DataStructures
author_profile: true
sidebar_main: true
# sidebar:
#     nav: "sidebar-category"
---

{% assign posts = site.categories.DataStructures %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}