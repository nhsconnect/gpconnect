---
title: Emergency codes
keywords: getcarerecord, view, section, allergies
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_emergency.html
summary: "Emergency codes HTML view"
---

{% include custominfocallout.html content="**Warning:** the Emergency codes section is only ever visible on the Summary view. It cannot be requested independently like the other HTML views." type="danger" %}


## Clinical narrative ##

During an emergency the Emergency codes section can be switched on and configured to display a known list of coded items, to enable a clinician to clearly see entries on the patient record associated with the emergency.

## Purpose ##

The purpose of this section is to provide the clinician with a list of configurable coded items during an emergency.

## Sections and subsections ##

There is a single main section for emergency codes with no subsections.

## Section title ##

The section title **MUST** be 'Emergency Codes'.

## Date filter ##

Date filters are not supported for this section all relevant records shall be returned.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.

## Table columns ##

Providers must return all the columns as described in the table below, sorted by `Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| 1 | `Date`  <em class="fa fa-sort-desc" aria-hidden="true"> | The date of entry of the coded item | `dd-Mmm-yyyy` |
| 2 | `Entry`| A short human readable title for the coded item | `free-text` |
| 3 | `Details` | Longer human readable details for the coded item | `free-text` |

## Additional functionality ##

The following two requirements **MUST** be fulfilled without need of code release:

 - The contents of this view **MUST** be based on a configurable list of codes
 - The Emergency codes view **MUST** contain configuration to allow the provider to switch on and off as necessary


## HTML view ##

{% include accessrecord/emergency.html %}

