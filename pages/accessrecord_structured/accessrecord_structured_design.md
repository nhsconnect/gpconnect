---
title: Access Record Structured design
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_design.html
summary: "Overview of the design decisions made in relation to the Access Record Structured capability"
published: false
---

## Access Record Structured capability scope ##

What is the scope of the Access Record Structured capability?

<span class="label label-info">DECISION</span> Currently, the Access Record Structured capability will return a patient’s allergies, medications, consultations, immunisations, problems and uncategorised data using the following FHIR&reg; profiles:

- AllergyIntolerance
- Medication
- Medication Statement
- Medication Request
- Encounter
- List
- Immunization
- ProblemHeader
- Observation
- Administrative profiles to support the above, as defined by the [Foundations capability pack](foundations.html)

{% include roadmap.html content="It is planned to include the remaining clinical areas of the patient record in future releases." %}

## FHIR profiles version ##

<span class="label label-info">DECISION</span> Standard for Trial Use 3 (STU3) is the version of FHIR which will be adopted for the Access Record Structured clinical profiles. A decision was taken to uplift the profiles from the previous DSTU2 version for the following reasons:

- STU3 is widely being adopted in the UK interoperability community
- there are many breaking changes between DSTU2 and STU3
- no supplier development had started on the previous DSTU2 versions
- the STU3 profiles offer additional clinical value

## Access Record Structured API definition ##

<span class="label label-info">DECISION</span> A review of the historic Access Record Structured maturity model has been completed. The following changes relating to the API have been agreed and the relevant implementation guidance applied throughout the Access Record Structured specification:

- the Access Record Structured clinical resources will be carried in a separate API message to the Access Record HTML resources
- API filtering will be introduced
- further filtering at the consumer end will be advocated (appropriate to the consumer need)
- consumers will be guided to return data for the patient in one (or few) round trips

{% include roadmap.html content="A RESTful model is still being considered. However, this has been removed from the short-term roadmap to allow time to evaluate the business need during the pilots." %}

## API search/filter parameters ##

<span class="label label-info">DECISION</span> Each clinical area will have its own set of search/filter parameters. These parameters will only apply to their own area. For example, a data filter set for medications will have no impact on the allergy data returned.

The benefits of this approach are:

- it is clear which search/filter parameters are applied to which clinical area
- adding or updating a search/filter parameter will only impact its own clinical area
- the search/filter parameters for a clinical area can be defined in parallel with their clinical area development

### API search/filter parameters for medications ###

- Date range based on
- Last Issue Date
- Effective Date where the last issue date is not available
- Record Date where the last issue date and effect date are not available
- Flag to include/exclude individual issues of a prescription

### API search/filter parameters for allergies ###

- None - there will be no date range applied for allergies due to clinical safety

{% include roadmap.html content="The definition of the API filter parameters for other clinical areas is in progress." %}

{% include note.html content="Search/filter parameters which were considered but not chosen for medications and allergies are: Fixed Date Range, SNOMED Code Cluster." %}

### API search/filter parameters for consultations ###

- date range for consultations
- number of most recent consultations to return

### API search/filter parameters for immunizations ###

- None - there will be no filtering applied to immunizations

### API search/filter parameters for problems ###

- clinical status of problem
- clinical significance of problem

### API search/filter parameters for uncategorised data ###

- date range for uncategorised data

 {% include note.html content="Search/filter parameters which were considered but not chosen for consultations, problems, immunisations and uncategorised data were retrieval by FHIR logical identifier. " %}

## Fabricated Consultations ##

Systems which allow direct recording of data outside of Consultation contexts should not fabricate Consultations to return such data. To do so would be generating information and structure which does not exist on the source system and would obscure the genuine Consultation content (for example, last X Consultations displayed in patient summaries). Systems in this category have clear distinctions between Consultations and other types of record content and to fabricate Consultations would distort this native behaviour.
