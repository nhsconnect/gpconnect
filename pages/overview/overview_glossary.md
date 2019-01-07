---
title: Glossary
keywords: abbreviations, definitions, glossaries, terms
tags: [getting_started]
sidebar: overview_sidebar
permalink: overview_glossary.html
summary: "Glossary of terms used in the GP Connect FHIR&reg; API specification"
toc: false
---

{% assign gloss = site.data.glossary | sort:'title' %}
{% for item in gloss %}

### {{ item.title }} ###

<p> {{ item.value }} </p>
 {{ item.html }} 

{% endfor %}
