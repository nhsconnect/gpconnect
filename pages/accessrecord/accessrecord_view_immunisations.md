---
title: Immunisations
keywords: getcarerecord, view, section, immunisations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_immunisations.html
summary: "Immunisations HTML view"
---

<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| IMM | Immunisations | Yes | Yes | Yes | Yes |

## Clinical narrative ##

Immunisation is the process whereby a person is treated to provide immunity or resistance to an infectious disease, typically by the administration of a vaccine.

## Purpose ##

The purpose of this section is to provide the health care professional with information about any immunisations that have been administered to the patient.

## Sections and subsections ##

There is only a single main section for the Immunisations section with no subsections.

### Date filter ###

Date filters are not supported for this section all relevant records shall be returned.

### Section content banner ###

Provider message(s) describing at a summary level how this section has been populated. Provider content messages can be found [here](accessrecord_provider_variance.html#immunisations).

### Table construction requirements ###

Providers **MUST** adhere to the table construction requirements listed below:

- table header **MUST** be "Immunisations"
- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

### Table columns ###

Providers **MUST** return all the columns as described in the table below, ordered by `Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` <i class="fa fa-sort-desc" aria-hidden="true"> | The date of the immunisation | `dd-Mmm-yyyy` |
| <center>2</center> | `Vaccination` | A short human readable free-text title for the immunisation | `free-text` |
| <center>3</center> | `Part` | Part number of immunisation | `integer` |
| <center>4</center> | `Contents` | Contents of the immunisation | `free-text` |
| <center>5</center> | `Details` | Longer human readable details for the immunisation | `free-text` |


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/immunisations.html %}

