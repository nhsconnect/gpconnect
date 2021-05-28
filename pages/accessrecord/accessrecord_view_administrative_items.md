---
title: Administrative items
keywords: getcarerecord, view, section, administrative items
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_administrative_items.html
summary: "Administrative Items HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ADM | Administrative Items | Yes | No<sup>1</sup> | Yes | Yes |

<sup>1</sup> EMIS have indicated they can't support extracting administrative items.

## Clinical narrative ##

These include tasks such as scheduling and administering clinical care encounters, clinical communication with other care organisations, administering and monitoring of critical safety processes such as repeat medication administration and call/recall for care.

## Purpose ##

The purpose of this section is to provide information for the health care teams on the recorded management and administrative processes and activity to support safe and effective care.

## Sections and subsections ##

There is only a single main section for Administrative Items with no subsections.

## Section title ##

The section title **MUST** be 'Administrative Items'.

## Date filter ##

A date filter is applicable for the Administrative Items section.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.

## Table columns ##

Providers **MUST** return all the columns as described in the table below, sorted by `Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| 1 | `Date`  <em class="fa fa-sort-desc" aria-hidden="true">| The date of the administrative item | `dd-Mmm-yyyy` |
| 2 | `Entry` | A short human readable free-text title for the administrative item | `free-text` |
| 3 | `Details` | Longer human readable details for the administrative item, codes such as READ or SNOMED **MUST NOT** be included. | `free-text` |

The provider **MAY** include or exclude items which are included in the [observations](accessrecord_view_observations.html) view.
If 'observations' are included, all the details which are included in the Value, Range and Details column **MUST** be included in the Details column.

## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/adminitems.html %}

## Example view ##

<p data-height="400" data-theme-id="light" data-slug-hash="QBoqNR" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Administrative Items" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/QBoqNR/">Allergies</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/QBoqNR) for example of using AngularJS to generate table content." %}
