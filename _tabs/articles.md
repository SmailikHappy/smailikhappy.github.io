---
title: "Articles"
layout: default
icon: fas fa-stream
order: 3
---

<h3>So far there are only few articles available</h3>

{% include lang.html %}

{% assign all_posts = site.posts | where: 'categories', 'Articles' %}

{% assign pinned = all_posts | where: 'pin', 'true' %}
{% assign default = all_posts | where_exp: 'item', 'item.pin != true and item.hidden != true' %}

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