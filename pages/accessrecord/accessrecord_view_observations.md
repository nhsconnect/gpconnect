---
title: Observations
keywords: getcarerecord, view, section, observations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_observations.html
summary: "Observations HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| OBS | Observations | Yes | Yes | Yes | Yes |

## Clinical narrative ##

A clinical observation is a repeatable data element recorded by health professionals in the course of assessment or care of their patients or clients. Examples include, blood pressure measurement, weight, height or temperature.

## Purpose ##

The purpose of this section is to enable the clinician to view and compare chronologically data recorded in structured form pertaining to a patient’s physical condition.

## Sections and subsections ##

There is only a single main section for observations with no subsections.

## Section title ##

The section title **MUST** be "Observations".

## Date filter ##

A date filter is applicable for the Observations section.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.

## Table columns ##

Providers must return all the columns as described in the table below, sorted by `Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date`  <i class="fa fa-sort-desc" aria-hidden="true">| The date of the observation | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry` | A short human readable free-text title for the observation | `free-text` |
| <center>3</center> | `Value` | Value and range (where available) of the observation | `free-text` |
| <center>4</center> | `Details` | Longer human readable details for the observation. Number formatting must follow the guidlines published on page 5 of the [CUI Medication Line] (http://webarchive.nationalarchives.gov.uk/20160921162642/http://systems.digital.nhs.uk/data/cui/uig/medlineqig.pdf) document.  | `free-text` |

{% include custominfocallout.html content="**Important:** GP principal suppliers have indicated this section will contain all clinical items that represent measurement data (for example, blood pressure, temperature, heart rate)." type="warning" %}
		
## HTML view ##

{% include accessrecord/observations.html %}

## Example view ##

<p data-height="425" data-theme-id="light" data-slug-hash="aENJMQ" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Observations" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/aENJMQ/">Observations</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/aENJMQ) for example of using AngularJS to generate table content." %}
