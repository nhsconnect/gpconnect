---
title: Referrals
keywords: getcarerecord, view, section, referrals
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_referrals.html
summary: "Referrals HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| REF | Referrals | Yes | Yes | Yes | Yes |

## Clinical narrative ##

This is a request for transfer of care or request to provide assessment, treatment or clinical advice on the care a patient.

## Purpose ##

The purpose of this section is to provide details of any referrals to or from other care providers.

## Sections and subsections ##

There is only a single main section for Referrals with no subsections.

## Section title ##

The section title **MUST** be 'Referrals'.

## Date filter ##

A date filter is applicable for the Referrals section.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.

## Table columns ##

Providers must return all the columns as described in the table below, sorted by `Date` descending:

<div>
<table>
<thead>
  <tr class="header">
	<th style="width:5%">Order</th>
	<th style="width:23%">Name</th>
	<th style="width:58%">Description</th>
	<th style="width:14%">Value details</th>
  </tr>
 </thead>
  <tr>
    <td style="text-align:center">1</td>
    <td><code>Date</code> <em class="fa fa-sort-desc" aria-hidden="true"></em></td>
    <td>The date of the referral</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr> 
  <tr>
    <td style="text-align:center">2</td>
    <td><code>From</code></td>
    <td>Practitioner or Organisation referred from</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">3</td>
    <td><code>To</code></td>
    <td>Practitioner or Organisation referred to </td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">4</td>
    <td><code>Priority</code></td>
    <td>The priority of the referral</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">5</td>
    <td><code>Details</code></td>
    <td>Longer human readable details for the referral
		<ul>
			<li>This <strong>MUST</strong> include all clinically relevant information about the referral which is not included in the other columns</li>
			<li>This <strong>MUST</strong> include the original term text for the main coded item describing the referral, which <strong>MUST</strong> be the first item</li>
			<li>Any additional information, such as the free text description of the referral, <strong>MUST</strong> separated from the original clinical term by a new line</li>
			<li>A label <strong>SHOULD</strong> preface additional information where necessary for reliable interpretation of the information</li>
		</ul>
	</td>
	<td><code>free-text</code></td>
  </tr>
</table>
</div>
 
  
## HTML view ##

{% include accessrecord/referrals.html %}

## Example view ##

<p data-height="580" data-theme-id="light" data-slug-hash="jYPVxN" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Referrals" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/jYPVxN/">Referrals</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/jYPVxN) for example of using AngularJS to generate table content." %}
