---
title: Emergency codes
keywords: getcarerecord, view, section, allergies
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_emergency.html
summary: "Emergency codes HTML view"
---

{% include custominfocallout.html content="**Warning:** the Emergency codes section is only ever visible on the Summary view. It cannot be requested independently like the other HTML views. Items in this view will also be visible in other HTML views." type="danger" %}


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
| 2 | `Entry`| Preferred term text for the coded item  | `free-text` |
| 3 | `Location` | The name of the HTML view(s) where this coded item is visible elsewhere in the record | `free-text` |

## Additional functionality ##

The following requirements **MUST** be fulfilled without need of code release:

 - The contents of this view **MUST** be based on a configurable list of codes.
 - The configurable list **MUST** be able to group codes to allow a single code to be visible, if more than one code in the group exits on the patient record. The most recent code on the record **MUST** be displayed in the Emergency Codes view.
 - The Emergency codes view **MUST** contain configuration to allow the provider to switch on and off as necessary.
 - The section content banner text **MUST** be a configurable item.

{% include custominfocallout.html content="**Information:** NHSD will supply the list of codes to be configured, and communicate when this functionality should be switch on/off." type="warning" %}
 
## HTML view ##

{% include accessrecord/emergency.html %}

