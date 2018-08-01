---
title: Glossary
keywords: abbreviations, definitions, glossaries, terms
tags: [getting_started]
sidebar: overview_sidebar
permalink: overview_glossary.html
summary: "Glossary of terms used by GP Connect"
toc: false
---

Glossary of common terms and abbreviations used though-out the GP Connect documentation.

<div>
{% assign gs = site.data.glossary | sort:[0] %}
{% for kv in gs %}
<dl>
  <dt>{{ kv[0] }}</dt>
  <dd>{{ kv[1] }}</dd>
</dl>
{% endfor %}
</div>
