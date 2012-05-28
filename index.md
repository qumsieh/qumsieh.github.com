---
layout: page
title: Ala's Blog
tagline: Stochastic Wanderings
---
{% include JB/setup %}

## Latest Posts:
<!--
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
-->
    
{% assign posts = site.posts %}
{% assign listing_limit = 5 %}
{% include Ala/post-listing.html %}
