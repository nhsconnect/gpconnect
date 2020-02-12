---
title: GP Connect API - Access Document 1.0.0-beta release notes
keywords: GP Connect, release notes
tags: [release]
sidebar: overview_sidebar
permalink: overview_release_notes_documents_1_0_0.html
summary: "GP Connect API - Access Document 1.0.0-beta released on 30th September 2019"
toc: false
---

{% include warning.html content="The seperate Access Document specification was merged into the GP Connect API specification at [GP Connect API 1.5.0](overview_release_notes_1_5_0.html#access-document). This page contains a release note from when the Access Document specification was versioned and published independently." %}

## Introduction ##

The GP Connect API - Access Document 1.0.0-beta release introduces the Access Document capability. This specification is being published separately to the other capabilities and looks purely at documents.

## Overview ##

### Getting started ###

**Affects**&nbsp; Overview

**Description:**

- page rewrite as other capabilities have been removed

**Pages changed:**

- [Getting started](overview_engage.html)

## Development ##

### General API guidance ###

**Affects**&nbsp; Development

**Description:**

- Service Root URL versioning - The `[PROVIDER_ROUTING_SEGMENT]` is now mandatory and is used to differentiate between logical FHIR servers that are exposed by providers
- The example service root URL has been updated to use a documents specific URL segment

**Pages changed:**

- [General API Guidance](development_general_api_guidance.html#service-root-url-versioning)

## Design approach ##

### API principles ###

**Affects**&nbsp; Design approach

**Description:**

- The first principle has been updated to state that this capability is exposed in it's own FHIR server.

**Pages changed:**

- [API design principles](designprinciples_open_api_principles.html)

## Spine integration ##

**Affects**&nbsp; Integrate with spine

**Description:**

- Interaction ids have been added for the query and retrieval APIs
- interaction ids have been added for the patient, organisation and practitioner APIs

**Pages changed:**

- [Interaction IDs](integration_interaction_ids.html)

## Access Record Documents ##

### Overview ###

### Use cases ###

### API ###

**Affects**&nbsp; Access Documents

**Description:**

- Restful APIs have been defined for querying and retrieving documents
- Restful APIs have been added for patient, organisation and practitioner
- Consumer sessions page has been added to illustrate how APIs are used

**Pages changed:**

- [Search for a patient's documents](access_documents_development_search_patient_documents.html)
- [Retrieve a patient's documents](access_documents_development_retrieve_patient_documents.html)
- [Consumer sessions illustrated](access_documents_development_api_session.html)
