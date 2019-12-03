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

A clinical observation is a repeatable data element recorded by health professionals in the course of assessment or care of their patients or clients. Examples include, blood pressure measurement, weight, height or temperature measurement.

## Purpose ##

The purpose of this section is to enable the clinician to view and compare chronological data pertaining to a patient's physical condition.

## Sections and subsections ##

There is only a single main section for observations with no subsections.

## Section title ##

The section title **MUST** be 'Observations'.

## Date filter ##

A date filter is applicable for the Observations section.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.

## Table columns ##

Providers must return all the columns as described in the table below, sorted by `Date` descending:

<div>
<table>
<thead>
  <tr class="header">
	<th width="5%">Order</th>
	<th width="23%">Name</th>
	<th width="58%">Description</th>
	<th width="14%">Value details</th>
  </tr>
 </thead>
  <tr>
    <td align="center">1</td>
    <td><code>Date</code> <em class="fa fa-sort-desc" aria-hidden="true"></em> </td>
    <td>The date of the observation</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr> 
  <tr>
    <td align="center">2</td>
    <td><code>Entry</code></td>
    <td>A short human readable free-text title for the observation</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td align="center">3</td>
    <td><code>Value</code></td>
	  <td>Value of the observation. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Value</li>
			<li>Value unit, where available</li>
		</ul>
	  </td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td align="center">4</td>
    <td><code>Range</code></td>
    <td>Range of the observation, where available. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Range</li>
			<li>Range unit, where available (unit <strong>MUST</strong> be included if it differs from the unit included in <code>Value</code>)</li>
		</ul>
	</td>
	<td><code>free-text</code></td>
  </tr>
  <tr>
    <td align="center">5</td>
    <td><code>Details</code></td>
    <td>Longer human readable details for the observation</td>
    <td><code>free-text</code></td>
  </tr>
</table>
</div>


{% include custominfocallout.html content="**Note:** All number formatting **MUST** follow the formatting applied in GP clinical supplier system providing the patient record." type="info" %}

{% include custominfocallout.html content="**Important:** GP principal suppliers have indicated this section will contain all clinical items that represent measurement data (for example, blood pressure, temperature, heart rate)." type="warning" %}
		
## HTML view ##

{% include accessrecord/observations.html %}

## Example view ##

<p data-height="475" data-theme-id="light" data-slug-hash="aENJMQ" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Observations" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/aENJMQ/">Observations</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/aENJMQ) for example of using AngularJS to generate table content." %}
