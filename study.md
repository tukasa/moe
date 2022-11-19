---
title: Study
layout: default
permalink: /study/
---
<h1 class="page-title">{{ page.title }}</h1>

<article class="post">
  <p>高度なカスタマイズと研究</p>
  <div class="post-content">
    <ul>
      {% for post in site.posts %}
      <li class="article-list">
      <time datetime="{{ page.date | date_to_xmlschema }}">{{ post.date | date: "%Y-%m-%d" }}</time> &raquo; <a href="{{ post.url  | relative_url }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ul>
  </div>
</article>