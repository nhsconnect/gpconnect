---
title: Implementation standards
keywords: 'getcarerecord, development, html, rendering'
sidebar: accessrecord_sidebar
permalink: accessrecord_development_html_implementation_guide.html
summary: >-
  Overview of the common HTML view rendering guidance in relation to the Access Record capability
tags:
  - development
  - getcarerecord
---

## HTML implementation standards ##

### Purpose ###

This document is intended for use by software developers, both provider supplier and consumer supplier, looking to build a conformant GP Connect HTML care record viewer application.

{% include custominfocallout.html content="**Information:** See section [HTML layout guide](accessrecord_development_html_layout_guide.html) for details of the layout of the HTML views." type="info" %}

### Notational conventions ###

The keywords "**MUST**", "**MUST NOT**", "**REQUIRED**", "**SHALL**", "**SHALL NOT**", "**SHOULD**", "**SHOULD NOT**", "**RECOMMENDED**", "**MAY**", and "**OPTIONAL**" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Near real time view ##

{% include custominfocallout.html content="**Information:** The record returned from the provider system is near real time." type="warning" %}

- local pending changes (that is, within a consultation that is actively ongoing) may not be available
- the record is machine-generated and therefore is not owned or attested by any single clinician

## Record locking ##

GP Connect queries/requests may be received while the patient's record is being updated.

Record locking inside a provider system **MUST NOT** impact the ability of the system to fulfil read/query requests of the patient's record.

However, it is understood that there are differing approaches to record locking within the GP principal systems which have an effect when any local/pending changes are actually committed back to the patient's record.

When a consumer system accesses a patient's record, the provider systems **MUST** only return data that has been successfully committed back to the patient's record and thus has become available to all users (including users of the provider APIs).

## Common user interface guidance ##

Where appropriate the following [Common User Interface (CUI)](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui) guidance documents should be followed when generating the GP Connect HTML views.

### NHS Number format ###

[NHS Number input and display](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/inputdisplay.pdf)<br/>
[NHS Number input and display - Quick Implementation Guide](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/inputdisplayqig.pdf)

### Patient details ###

[Patient Name input and display](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/patnamedisp.pdf)<br/>
[Patient Name input and display - Quick Implementation Guide](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/patnamedispqig.pdf)

[Sex and current Gender input and display](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/sex.pdf)<br/>
[Sex and current Gender input and display - Quick Implementation Guide](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/sexqig.pdf)

### Date/time format ###

[Date display](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf)<br/>
[Time display](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/timedisplay.pdf)<br/>
[Date Time display - Quick Implementation Guide](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/datetimedispqig.pdf)

### GP details ###

[Address input and display](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/address.pdf)<br/>
[Telephone Number input and display](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/tele.pdf)

### Medication representation ###

[Medications Management - Medication Line](https://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/medline.pdf)

{% include custominfocallout.html content="**Note:** All number formatting **MUST** follow the formatting applied in GP clinical supplier system providing the patient record. All units **MUST** be displayed, where available. " type="info" %}

## Patient banner ##

Consumer systems **MUST** present a patient banner above the HTML content returned from the GP Connect APIs in line with the CUI guidance.

[Patient Banner](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/patben.pdf)<br/>
[Patient Banner - Quick Implementation Guide](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/patben.pdf)


## Minimum display resolution ##

This guidance is applicable to user interfaces displayed on desktop or laptop computers. It is assumed that, at a minimum, these computers are capable of operating at a minimum display resolution of **1024 x 768** and have a keyboard and pointing device.

## Structured data ##

### FHIR resources ###

Provider systems **MUST** return a minimal set of structured data along with the HTML content as follows:

| FHIR resource(s) | Composition section  |
|------------------|--------|-------------|
| `Patient`        | Subject              |
| `Practitioner`   | User                 |
| `Organization`   | Custodian            |
| `Device`         | Author<sup>1</sup>   |

<sup>1</sup> As the composition is machine-generated the concept of a single Author does not make logical sense. It is expected that the Author field will be populated with the details of the software system which generated the composition.

### Demographic cross checking ###

Consumer systems **MUST** compare the returned structured patient demographic data (supplied by the provider system as structured data) against the demographic data held in the consumer system.

If differences exist then the consumer system **MUST** show an alert/warning and provide details of which fields/values are different between the two systems.

The following data **MUST** be cross checked between consumer and returned provider data. Any differences between these fields **MUST** be brought to the attention of the user.   

| Item | Resource element |
| ---- | -------------- |
| Family Name | `Patient.name.family` |
| Given Name | `Patient.name.given` |
| Gender | `Patient.gender` |
| Birth Date | `Patient.birthDate` |
| GP Practice Code | `Patient.managingOrganization` |
| Deceased Date Time | `Patient.deceased[x](deceasedDateTime)` |  

Additionally, the following data **MAY** be displayed if returned from the provider to assist a visual cross check and for safe identification but should not be part of the automatic comparison.

* Address and Postcode
* Contact (telephone, mobile, email)
* Responsible GP Code and Name
* GP Practice Name and Address

Where a patient is flagged on the GP clinical system as sensitive (and as such the GP practice must not identify that the patient is registered at this location), the provider system **MUST NOT** return any clinical records and instead return the error `Patient not found`.

Where a patient is flagged on the Personal Demographics Service (PDS) as sensitive (and as such it is not possible to confirm their registered GP practice), the consumer system **MUST NOT** use GP Connect.

## Section retrieval ##

The consuming system **MUST** provide role based access controls to the HTML section retrieval at an appropriate level such that the consuming organisation can meet its obligations as described in the [Information governance principles](designprinciples_ig_principles.html) page.

The consuming organisation **MUST** provide appropriate support to its users to understand the error messages associated with the HTML sections as follows.

### Error handling ###

If a GP principal system can't meaningfully supply content for a requested HTML section (or subset of the Summary View) then the system **MUST** return the following HTML fragment in place of the HTML table.

#### Supported but hasn't been recorded ####

- system can store the data
- BUT no data has been recorded for the patient

```html
<div>
	<p>No '[section]' data is recorded for this patient.</p>
</div>
```

#### Supported but can't be technically provided ####

- system can store the data
- BUT no data is available for the patient via the GP Connect APIs due to a technical limitation

```html
<div>
	<p>This system does not support retrieval of '[section]' data.</p>
	<p>This data may still exist in the source system.</p>
</div>
```

#### Supported but is masked/access denied ####

- system can store the data
- BUT no data is available for the patient via the GP Connect APIs due to an IG/DS rule

```html
<div>
	<p>Access is denied to '[section]' data for this patient.</p>
	<p>This data may still exist in the source system.</p>
</div>
```

#### Not supported ####

- system doesn't store the data

```html
<div>
	<p>'[section]' data is not supported by this system.</p>
</div>
```

# HTML section views #

Provider systems **MUST** use XHTML constructs as defined in the [FHIR narrative](https://www.hl7.org/fhir/narrative.html) guidance contained within the FHIR&reg; standard.

## [XHTML narrative](https://www.hl7.org/fhir/narrative.html) ##

As outlined in the Narrative section of the FHIR&reg; standard:

{% include callout.html content="The XHTML content **MUST NOT** contain a head, a body element, external stylesheet references, deprecated elements, scripts, forms, base/link/xlink, frames, iframes, objects or event related attributes (for example, onClick). This is to ensure that the content of the narrative is contained within the resource and that there is no active content. Such content would introduce security issues and potentially safety issues with regard to extracting text from the XHTML.<br/><br/> Note that the XHTML is contained in general XML so there is no support for HTML entities like ```&nbsp;``` or ```&copy;```. Unicode characters **MUST** be used instead. Unicode ```&#160;``` substitutes for ```&nbsp;```." type="default" %}

{% include custominfocallout.html content="**Information:** The content **MUST NOT** contain any platform-specific escape or formatting characters such as ```\r\n```, as these may cause inconsistent rendering within consumer applications, with potential impacts on clinical safety." type="warning" %}

## [Styling the XHTML](https://www.hl7.org/fhir/narrative.html#css) ##

As outlined in the 'Styling the XHTML' section of the FHIR&reg; standard:

{% include callout.html content="In order to minimise manageability and security issues, authoring systems cannot specify the CSS stylesheet to use directly. Instead, the application that displays the resource provides the stylesheets. This means that the rendering system chooses what styles can be used, but the authoring system must use them in advance. Authoring systems can use these classes, which **MUST** be supported by all rendering systems.<br/><br/> Please see the [FHIR Runtime CSS](https://www.hl7.org/fhir/stu3/fhir-runtime.css) or [Styling the XHTML](https://www.hl7.org/fhir/narrative.html#css) on the FHIR website for full details." type="default" %}

## CSS IDs and classes  ##

The following HTML IDs **MUST** be applied across the HTML views:


| ID name            | Description                                                                              | HTML view(s)
| ------------------ | ---------------------------------------------------------------------------------------- | --------------------------------------
| `adm-tab`          | Applied within the `<table>` tag of the Administrative Items table                       | Administrative Items
| `all-tab-curr`     | Applied within the `<table>` tag of the Current Allergies and Adverse Reactions table    | Allergies and Adverse Reactions & Summary
| `all-tab-hist`     | Applied within the `<table>` tag of the Historical Allergies and Adverse Reactions table | Allergies and Adverse Reactions
| `cli-tab`          | Applied within the `<table>` tag of the Clinical Item table and Summary (Emergency Codes)| Clinical Items & Summary (Emergency Codes)
| `enc-tab`          | Applied within the `<table>` tag of the Encounters table                                 | Encounters & Summary
| `imm-tab`          | Applied within the `<table>` tag of the Immunisations table                              | Immunisations
| `med-tab-acu-med`  | Applied within the `<table>` tag of the Acute Medication (Last 12 Months)                | Medications & Summary
| `med-tab-curr-rep` | Applied within the `<table>` tag of the Current Repeat Medication table                  | Medications & Summary
| `med-tab-dis-rep`  | Applied within the `<table>` tag of the Discontinued Repeat Medication table             | Medications
| `med-tab-all-sum`  | Applied within the `<table>` tag of the All Medication table                             | Medications
| `med-tab-all-iss`  | Applied within the `<table>` tag of the All Medication Issues table                      | Medications
| `obs-tab`          | Applied within the `<table>` tag of the Observations table                               | Observations
| `prb-tab-act`      | Applied within the `<table>` tag of the Active Problems and Issues table                 | Problems and Issues & Summary
| `prb-tab-majinact` | Applied within the `<table>` tag of the Major Inactive Problems and Issues table         | Problems and Issues & Summary
| `prb-tab-othinact` | Applied within the `<table>` tag of the Other Inactive Problems and Issues table         | Problems and Issues
| `ref-tab`          | Applied within the `<table>` tag of the Referrals table                                  | Referrals

<br/>

The following HTML classes **MUST** be applied across the HTML view:


| Class name         | Description                                                                              | HTML view(s)
| ------------------ | ---------------------------------------------------------------------------------------- | --------------------------------------
| `content-banner`   | Applied within the `<div>` tag of any section/subsection content banner                  | All views
| `date-banner`      | Applied within the `<div>` tag of any section/subsection date filter banner              | All views
| `exclusion-banner` | Applied within the `<div>` tag of any section/subsection exclusion banner                | All views
| `gptransfer-banner`| Applied within the `<div>` tag of any section/subsection exclusion banner                | All views
| `date-column` 	 | Applied within the `<td>` tag of any table column with a `dd-Mmm-yyyy` date format       | All views
| `med-item-column`  | Applied within the `<td>` tag of a grouped distinct `Medication Item`       				| Medications (All Medication (Summary) & All Medication Issues only)
