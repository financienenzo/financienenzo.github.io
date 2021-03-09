---
layout: page
title: Over
comments: false
---

This website is built with Jekyll and "Affiliates" (a Jekyll Template designed & developed by WowThemes.net). It is meant for demonstration purposes, so you can have an idea of how this theme looks in action so no real content can be found. Affiliates template for Jekyll is compatible with Github pages, in fact even this demo is created with Github Pages and hosted with Github. This page in example shows a page layout.

<ul>
  {% for author in site.authors %}
    <li>
      <h2>{{ author.name }}</h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>
