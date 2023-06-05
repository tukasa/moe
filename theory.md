---
layout: default
title: 理論
auther: tukasa
folder: theory
permalink: /theory/
---

<h1>{{ page.title }}</h1>

{% for collection in site.collections %}
  {% if collection.label == page.folder %}
    {% assign groups = collection.docs | group_by: "part" %}
    {% assign date_now = site.time | date: "%y%m" | to_integer %}
  {% endif %}
{% endfor %}

{% for group in groups %}
  <h2 id="{{ group.name }}">{{ group.name }}</h2>
  <ul>
  {% assign chapter = group.items | sort: "path" %}
  {% for item in chapter %}
    <li class="post-list-by-part">
       {% assign new_post = "" %}
       {% if item.last_modified_at %}
         {% assign date_post = item.last_modified_at | date: "%y%m" | plus: 1 %}
       {% else %}
         {% assign date_post = item.created_at | date: "%y%m" | plus: 1 %}
       {% endif %}
       <a href="{{ item.url | relative_url }}">{{ item.title }}</a>
         {% if date_post >= date_now %}
           {% assign new_post = ":sparkles:" %}
         {% endif %}
       <span>{{ new_post }}
       <time datetime="{{ page.date | date_to_xmlschema }}">
       {% if item.last_modified_at %}
         {{ item.last_modified_at }}
       {% else %}
         {{ item.created_at }}
       {% endif %}
       </time>
       </span>
    </li>
  {% endfor %}
  </ul>
{% endfor %}