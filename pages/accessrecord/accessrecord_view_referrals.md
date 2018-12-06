---
title: Referrals
keywords: getcarerecord, view, section, referrals
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_referrals.html
summary: "Referrals HTML view"
---

<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| REF | Referrals | Yes | Yes | Yes | Yes |

## Clinical narrative ##

This is a request for transfer of care or request to provide assessment, treatment or clinical advice on the care a patient.

## Purpose ##

The purpose of this section is to provide details of any referrals to or from other care providers.

## Sections and subsections ##

There is only a single main section for Referrals with no subsections.

### Date filter ###

A date filter is applicable for the Referrals section. Provider messages for a date filter can be found [here](accessrecord_provider_variance.html#date-banner-message).

### Section content banner ###

Provider message(s) describing at a summary level how this section has been populated. Provider content messages can be found [here](accessrecord_provider_variance.html#referrals).

### Table construction requirements ###

Providers **MUST** adhere to the table construction requirements listed below:

- table header **MUST** be "Referrals"
- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

### Table columns ###

Providers **MUST** return all the columns as described in the table below, ordered by `Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date`  <i class="fa fa-sort-desc" aria-hidden="true"> | The date of the referral | `dd-Mmm-yyyy` |
| <center>2</center> | `From` | Practitioner and/or Organization referred from | `free-text` |
| <center>3</center> | `To` | Practitioner and/or Organization referred to | `free-text` |
| <center>4</center> | `Priority` | The priority of the referral | `free-text` |
| <center>5</center> | `Details` | Longer human readable details for the referral | `free-text` |


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/referrals.html %}
