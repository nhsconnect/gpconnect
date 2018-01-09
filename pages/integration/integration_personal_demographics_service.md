---
title: Personal Demographic Service
keywords: spine, pds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_personal_demographic_service.html
summary: "Overview of the role of the Personal Demographic Services (PDS) and the Spine Mini Services PDS (SMSP) within GP Connect."
---

## PDS tracing ##

GP Connect systems SHALL be capable of performing [Personal Demographic Service](https://digital.nhs.uk/Demographics){:target="_blank"} (PDS) tracing of patients to obtain their NHS number, date of birth and current GP organisation.

Systems SHALL perform this tracing using one of the following three options:

### 1. Full PDS Spine compliant system ###


GP Connect systems MAY follow the guiding principles of [how systems should integrate with PDS](http://webarchive.nationalarchives.gov.uk/20160921135209/http://systems.digital.nhs.uk/demographics/spineconnect). This describes in particular the principles governing how systems should synchronise with PDS as the master repository of demographics data to ensure local system data does not become stale.

There is a very limited risk that the consumer-traced NHS number pre-dates a patient record status change to sensitive Flag (S-Flag) immediately prior to use.

### 2. Spine Mini Service PDS (SMSP) ###

GP Connect systems MAY utilise the [Spine Mini Service Provider for PDS](https://developer.nhs.uk/library/systems/nhs-digital-smsp-pds/){:target="_blank"} (SMSP) as a lighter weight alternative to integrating with the full Spine PDS.


{% include important.html content="As the SMSP service does not return multiple possible matches for the patient it is typically only suitable to be used where there is enough information to achieve a single matched trace." %}

{% include note.html content="SMSP responses do not include trace sequence number information. The presence of a trace sequence number in a consumer request to GP Connect could enable providers to programmatically determine the need to perform a PDS trace themselves, for example if their local patient record's trace was not current." %}


### Demographics Batch Service (DBS) ###

GP Connect systems MAY utilise the [Demographics Batch Service (DBS)](http://developer.nhs.uk/library/systems/demographic-batch-service-dbs/){:target="_blank"} to perform batch PDS tracing.

The suitability of the use of DBS to perform batch PDS tracing would be assessed as part of the consumer accreditation process.
