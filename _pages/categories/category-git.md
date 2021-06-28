---
title: "Git/GitHub"
layout: archive
permalink: categories/git
author_profile: true
sidebar_main: true
---

<!-- site.categories.Git 이 부분이 post내에 있는 category에서 고르는 것 같다. -->

{% assign posts = site.categories.git %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
