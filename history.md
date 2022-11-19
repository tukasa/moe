---
layout: default
title: 知的生産の技術の歴史
auther: tukasa
folder: history
permalink: /history/
---

<h1>{{ page.title }}</h1>

{% for collection in site.collections %}
  {% if collection.label == page.folder %}
    {% assign groups = collection.docs | group_by: "part" %}
  {% endif %}
{% endfor %}

{% for group in groups %}
  <h2 id="{{ group.name }}">{{ group.name }}</h2>
  <ul>
  {% assign chapter = group.items | sort: "path" %}
  {% for item in chapter %}
    <li class="post-list-by-part">
       <a href="{{ item.url | relative_url }}">{{ item.title }}</a>
       <time datetime="{{ page.date | date_to_xmlschema }}">
       {% if item.last_modified_at %}
         {{ item.last_modified_at }}
       {% else %}
         {{ item.date | date: "%Y-%m-%d" }}
       {% endif %}
       </time>
    </li>
  {% endfor %}
  </ul>
{% endfor %}