---
title: Glossary
keywords: abbreviations, definitions, glossaries, terms
tags: [getting_started]
sidebar: overview_sidebar
permalink: overview_glossary.html
summary: "Glossary of terms used by the GP Connect Messaging specification"
toc: false
---

<div>
{% assign gloss = site.data.glossary.glossary | sort:'title' %}
{% for item in gloss %}
<dl>
  <dt><h3>{{ item.title }}</h3></dt>
  <dd>{{ item.value }}</dd>
</dl>
{% endfor %}
</div>
