---
title: "Projects"
layout: default
icon: fas fa-stream
order: 1
---

{% include lang.html %}

{% assign pinned = site.posts | where: 'pin', 'true' %}
{% assign default = site.posts | where_exp: 'item', 'item.pin != true and item.hidden != true' %}

{% assign posts = pinned | concat: default %}

<div id="post-list" class="flex-grow-1 px-xl-1">
  {% for post in posts %}
    {% include post-card.html %}
  {% endfor %}
</div>
<!-- #post-list -->

{% if paginator.total_pages > 1 %}
  {% include post-paginator.html %}
{% endif %}