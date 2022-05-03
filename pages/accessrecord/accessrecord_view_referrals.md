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

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| 1 | `Date`  <em class="fa fa-sort-desc" aria-hidden="true">| The date of the referral | `dd-Mmm-yyyy` |
| 2 | `From` | Practitioner or Organisation referred from | `free-text` |
| 3 | `To` | Practitioner or Organisation referred to | `free-text` |
| 4 | `Priority` | The priority of the referral | `free-text` |
| 5 | `Details` | Longer human readable details for the referral | `free-text` |

## HTML view ##

{% include accessrecord/referrals.html %}

## Example view ##

<p data-height="580" data-theme-id="light" data-slug-hash="jYPVxN" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Referrals" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/jYPVxN/">Referrals</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/jYPVxN) for example of using AngularJS to generate table content." %}
