---
layout: page
permalink: /news/
title: news
description: Talks, papers and other updates.
nav: true
nav_order: 2
---

<div class="news-archive">
{%- assign items = site.news | sort: 'date' | reverse -%}
{%- for item in items %}
  <div class="news-row">
    <div class="news-date">{{ item.date | date: "%b %-d, %Y" }}</div>
    <div class="news-body">
      {%- if item.inline -%}
        {{ item.content | emojify }}
      {%- else -%}
        <a class="news-title" href="{{ item.url | relative_url }}">{{ item.title }}</a>
        {{ item.content | emojify }}
      {%- endif -%}
    </div>
  </div>
{%- endfor %}
</div>
