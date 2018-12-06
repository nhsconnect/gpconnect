---
title: Administrative items
keywords: getcarerecord, view, section, administrative items
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_administrative_items.html
summary: "Administrative Items HTML view"
---

<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ADM | Administrative Items | Yes | No<sup>1</sup> | Yes | Yes |

<sup>1</sup> EMIS have indicated they can't support extracting administrative items.

## Clinical narrative ##

These include tasks such as scheduling and administering clinical care encounters, Clinical communication with other care organisations, administering and monitoring of critical safety processes such as repeat medication administration and call/recall for care.

## Purpose ##

The purpose of this section is to provide information for the health care teams on the recorded management and administrative processes and activity to support safe and effective care.

## Sections and subsections ##

There is only a single main section for Administrative Items with no subsections.

### Date filter ###

A date filter is applicable for the Administrative Items section. Provider messages for a date filter can be found [here](accessrecord_provider_variance.html#date-banner-message).

### Section content banner ###

Provider message(s) describing at a summary level how this section has been populated. Provider content messages can be found [here](accessrecord_provider_variance.html#administrative-items).

### Table construction requirements ###

Providers **MUST** adhere to the table construction requirements listed below:

- table header **MUST** be "Administrative Items"
- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

### Table columns ###

Providers **MUST** return all the columns as described in the table below, ordered by `Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` <i class="fa fa-sort-desc" aria-hidden="true"> | The date of the administrative item | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry` | A short human readable free-text title for the administrative item | `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the administrative item, codes such as READ or SNOMED **MUST NOT** be included. | `free-text` |



## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/adminitems.html %}


