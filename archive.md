---
layout: page
title: Archive
author: Carlos Alves
tags: about
---

<center><h1> Blog Posts </h1></center>

<!-- Look the author details up from the site config. -->
{% assign author = site.data.authors[page.author] %}

<ul class="post-list" itemscope itemtype="http://schema.org/Blog">
  {% for post in site.posts %}
    <li itemprop="blogPost" itemscope itemtype="http://schema.org/BlogPosting">
      <span class="post-meta"><time itemprop="datePublished" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d, %Y" }}</time></span>
      <h2>
              <a class="post-link" href="{{ post.url | prepend: site.baseurl }}" itemprop="url"><span itemprop="name headline">{{ post.title }}</span></a>
      </h2>

      <div itemprop="description">{{ post.excerpt }}</div>
   </li>
  {% endfor %}
</ul> 
