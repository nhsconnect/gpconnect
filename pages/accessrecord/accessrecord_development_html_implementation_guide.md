---
title: HTML Implementation Standards
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

This document is intended for use by software developers looking to build a conformant GP Connect HTML care record viewer application.

{% include custominfocallout.html content="**Information:** See section [HTML layout guide](accessrecord_development_html_layout_guide.html) for details of the layout of the HTML views." type="info" %}

### Notational conventions ###

The keywords "**MUST**", "**MUST NOT**", "**REQUIRED**", "**SHALL**", "**SHALL NOT**", "**SHOULD**", "**SHOULD NOT**", "**RECOMMENDED**", "**MAY**", and "**OPTIONAL**" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Near real time view ##

{% include custominfocallout.html content="**Information:** The record returned from the provider system is near real time." type="warning" %}

- Local pending changes (that is, within a consultation that is actively ongoing) may not be available.
- The record is machine generated and therefore is not owned or attested by any single clinician.

## Record locking ##

GP Connect queries/requests may be received while the patient's record is being updated.

Record locking inside a provider system **SHALL NOT** impact the ability of the system to fulfil read/query requests of the patient's record.

However, it is understood that there are differing approaches to record locking within the GP principal systems which have an effect when any local/pending changes are actually committed back to the patient's record.

When a consumer system accesses a patient's record, the provider systems **SHALL** only return data that has been successfully committed back to the patient's record and thus has become available to all users (including users of the provider APIs).

## Common user interface guidance ##

Where appropriate the following [Common User Interface (CUI)](https://digital.nhs.uk/data-and-information/information-standards/common-user-interface-cui) guidance documents should be followed when generating the GP Connect HTML views.

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

## Patient banner ##

Consumer systems **SHALL** present a patient banner above the HTML content returned from the GP Connect APIs in line with the CUI guidance.

[Patient Banner](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/patben.pdf)<br/>
[Patient Banner - Quick Implementation Guide](http://webarchive.nationalarchives.gov.uk/20160921150545/http://systems.digital.nhs.uk/data/cui/uig/patben.pdf)

## Minimum display resolution ##

This guidance is applicable to user interfaces displayed on desktop or laptop computers. It is assumed that, at a minimum, these computers are capable of operating at a minimum display resolution of **1024 x 768** and have a keyboard and pointing device.

## Structured data ##

### FHIR resources ###

Provider systems **SHALL** return a minimal set of structured data along with the HTML content as follows:

| FHIR resource(s) | Composition section  |
|------------------|--------|-------------|
| `Patient`          | Subject              |
| `Practitioner`     |                      |
| `Organization`     | Custodian            |
| `Device`           | Author<sup>1</sup>   |

<sup>1</sup> As the composition is machine-generated the concept of a single Author does not make logical sense. It is expected that the Author field will be populated with the details of the software system which generated the composition.

### Demographic cross checking ###

Consumer systems **SHALL** compare the returned structured patient demographic data (supplied by the provider system as structured data) against the demographic data held in the consumer system.

If differences exist then the consumer system **SHALL** show an alert/warning and provide details of which fields/values are different between the two systems.

The following data **SHALL** be cross checked between consumer and returned provider data. Any differences between these fields **SHALL** be brought to the attention of the user.   

| Item | Resource field |
| ---- | -------------- | 
| Family Name | patient.name.family |
| Given Name | patient.name.given |
| Gender | patient.gender |
| Birth Date | patient.birthDate |
| GP Practice Code | patient.managingOrganization | 

<sup>1</sup>May be redacted if patient is flagged on Spine as Sensitive demographics.

Additionally, the following data **MAY** be displayed if returned from the provider to assist a visual cross check and for safe identification but should not be part of the automatic comparison.

* Address and Postcode
* Contact (telephone, mobile, email)
* Responsible GP Code and Name
* GP Practice Name and Address

All above may be redacted if patient is flagged on Spine as Sensitive demographics.

## Section retrieval ##

### Error handling ###

If a GP principal system can't meaningfully supply content for a requested HTML section (or subset of the Summary View) then the system **SHALL** return the following HTML fragment in place of the HTML table.

#### Supported but hasn't been recorded ####

- System can store the data.
- BUT no data has been recorded for the patient.

```html
<div>
	<p>No '[section]' data is recorded for this patient.</p>
</div>
```

#### Supported but can't be technically provided ####

- System can store the data.
- BUT no data is available for the patient via the GP Connect APIs due to a technical limitation.

```html
<div>
	<p>This system does not support retrieval of '[section]' data.</p>
	<p>This data may still exist in the source system.</p>
</div>
```

#### Supported but is masked/access denied ####

- System can store the data.
- BUT no data is available for the patient via the GP Connect APIs due to a IG/DS rule.

```html
<div>
	<p>Access is denied to '[section]' data for this patient.</p>
	<p>This data may still exist in the source system.</p>
</div>
```

#### Not supported ####

- System doesn't store the data.

```html
<div>
	<p>'[section]' data is not supported by this system.</p>
</div>
```

# HTML section views #

Provider systems **SHALL** use XHTML constructs as defined in the [FHIR narrative](https://www.hl7.org/fhir/narrative.html) guidance contained within the FHIR&reg; standard.

### [XHTML narrative](https://www.hl7.org/fhir/narrative.html) ###

As outlined in the Narrative section of the FHIR&reg; standard:

{% include callout.html content="The XHTML content **SHALL NOT** contain a head, a body element, external stylesheet references, deprecated elements, scripts, forms, base/link/xlink, frames, iframes, objects or event related attributes (e.g. onClick). This is to ensure that the content of the narrative is contained within the resource and that there is no active content. Such content would introduce security issues and potentially safety issues with regard to extracting text from the XHTML.<br/><br/> Note that the XHTML is contained in general XML so there is no support for HTML entities like ```&nbsp;``` or ```&copy;``` etc. Unicode characters **SHALL** be used instead. Unicode ```&#160;``` substitutes for ```&nbsp;```." type="default" %}

{% include custominfocallout.html content="**Information:** The content **SHALL NOT** contain any platform-specific escape or formatting characters such as ```\r\n```, as these may cause inconsistent rendering within consumer applications, with potential impacts on clinical safety." type="warning" %}

### [Styling the XHTML](https://www.hl7.org/fhir/narrative.html#css) ###

As outlined in the 'Styling the XHTML' section of the FHIR&reg; standard:

{% include callout.html content="In order to minimise manageability and security issues, authoring systems cannot specify the CSS stylesheet to use directly. Instead, the application that displays the resource provides the stylesheets. This means that the rendering system chooses what styles can be used, but the authoring system must use them in advance. Authoring systems can use these classes, which **SHALL** be supported by all rendering systems.<br/><br/> Please see the [FHIR Runtime CSS](https://www.hl7.org/fhir/stu3/fhir-runtime.css) or [Styling the XHTML](https://www.hl7.org/fhir/narrative.html#css) on the FHIR website for full details." type="default" %}
