---
layout: default
title: Table of Contents
description: All posts in one place
permalink: /toc
---

# Table of Contents

{% for post in site.posts %}
  <h2 class="fs-4 mt-4">
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <span class="fs-6"> -> {{ post.date | date: "%B %-d, %Y" }}</span>
  </h2>
  <p>{{post.description}}</p>
{% endfor %}
