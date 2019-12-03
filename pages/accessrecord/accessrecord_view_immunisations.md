---
title: Immunisations
keywords: getcarerecord, view, section, immunisations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_immunisations.html
summary: "Immunisations HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| IMM | Immunisations | Yes | Yes | Yes | Yes |

## Clinical narrative ##

Immunisation is the process whereby a person is treated to provide immunity or resistance to an infectious disease, typically by the administration of a vaccine.

## Purpose ##

The purpose of this section is to provide the health care professional with information about any immunisations that have been administered to the patient.

## Sections and subsections ##

There is only a single main section for the Immunisations section with no subsections.

## Section title ##

The section title **MUST** be 'Immunisations'.

## Date filter ##

Date filters are not supported for this section all relevant records shall be returned.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.

## Table columns ##

Providers must return all the columns as described in the table below, sorted by `Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date`  <em class="fa fa-sort-desc" aria-hidden="true">| The date of the immunisation | `dd-Mmm-yyyy` |
| <center>2</center> | `Vaccination` | A short human readable free-text title for the immunisation | `free-text` |
| <center>3</center> | `Part` | Part number of immunisation | `integer` |
| <center>4</center> | `Contents` | Contents of the immunisation | `free-text` |
| <center>5</center> | `Details` | Longer human readable details for the immunisation | `free-text` |

## HTML view ##

{% include accessrecord/immunisations.html %}

## Example view ##

<p data-height="425" data-theme-id="light" data-slug-hash="MXxLwX" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Immunisations" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/MXxLwX/">Immunisations</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/MXxLwX) for example of using AngularJS to generate table content." %}
