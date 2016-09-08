---
title: Resource Guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_resource_guidance.html
summary: "Details of what resources and operations a FHIR server should expose to be a fully compliant GP Connect solution."
---

{% include tip.html content="Refer to the [Explore - Swagger API Documentation](system_reference_swagger.html) for further details." %}

## Foundation Resources ##

4 of the following 4 resources are expected to have their own API endpoints for GP Connect FoT.

| Resource | Create | Read | Update | Delete | History<br/>Read | Search | Identifier<br/>Search | Bundle<br/>Read | Compartment<br/>Read |  
|----------|--------|------|--------|--------|------------------|--------|-----------------------|-----------------|----------------------|
| [Organization](https://www.hl7.org/fhir/DSTU2/organization.html) | &nbsp; | Yes | &nbsp; | &nbsp; | &nbsp; | &nbsp; | `ODSCode` | `$gpc.getcarerecord` | &nbsp; |
| [Patient](https://www.hl7.org/fhir/DSTU2/patient.html) | &nbsp; | Yes | &nbsp; | &nbsp; | &nbsp; | &nbsp; | `NHSNumber` | `$gpc.getcarerecord`<br/>`$gpc.registerpatient` | &nbsp; |
| [Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html) | &nbsp; | Yes | &nbsp; | &nbsp; | &nbsp; | &nbsp;  | `SDSUserID` | `$gpc.getcarerecord`<br/>`$gpc.getschedule` | &nbsp; |
| [Location](https://www.hl7.org/fhir/DSTU2/location.html) | &nbsp; | &nbsp; | &nbsp; | &nbsp;| &nbsp; | &nbsp; | `ODSSiteCode` | `$gpc.getschedule` | &nbsp; |

Refer to [Capability Pack - Foundations](foundations.html) for further details.

## Access Care Record Resources ##

{% include important.html content="NHS Digital facilitated workshops will be being run throughout August and September to finalise the GP Connect FHIR profiles. [Structured Data](accessrecord_structured_data_summary.html) access remains a high priority for the GP Connect programme however we have temporarily removed the majority of the structured resources from the [Access Record FHIR API IG / DMS Bundle](http://data.developer.nhs.uk/fhir/candidaterelease-170816-getrecord/index.html) to enable development to commence on the [Access Record HTML Views](accessrecord_view_summary.html)." %}

0 of the following 13 resources are expected to have their own API endpoints for GP Connect FoT ([Stage 1. Maturity Model](designprinciples_maturity_model.html)).

| Resource | Create | Read | Update | Delete | History<br/>Read | Search | Identifier<br/>Search | Bundle<br/>Read | Compartment<br/>Read |  
|----------|--------|------|--------|--------|------------------|--------|-----------------------|-----------------|----------------------|
|Coming soon. <br> Please refer to [DMS Bundle](http://data.developer.nhs.uk/fhir/candidaterelease-170816-getrecord/index.html) | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | `$gpc.getcarerecord` | &nbsp; |

Refer to [Capability Pack - Access Record](accessrecord.html) for further details.

## Appointment Management Resources ##

1 of the following 3 resources are expected to have their own API endpoints for GP Connect FoT.

| Resource | Create | Read | Update | Delete | History<br/>Read | Search | Identifier<br/>Search | Bundle<br/>Read | Compartment<br/>Read |  
|----------|--------|------|--------|--------|------------------|--------|-----------------------|-----------------|----------------------|
| [Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html) | Yes | Yes | Yes | &nbsp; | Current | &nbsp; | NHSNumber | &nbsp; | Patient |
| [Schedule](https://www.hl7.org/fhir/DSTU2/schedule.html) | &nbsp; | &nbsp; | &nbsp; | &nbsp;| &nbsp; | &nbsp; | &nbsp; | `$gpc.getschedule` | &nbsp; |
| [Slot](https://www.hl7.org/fhir/DSTU2/slot.html) | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp;| &nbsp; | &nbsp; | `$gpc.getschedule` | &nbsp; |

Refer to [Capability Pack - Appointment Management](appointments.html) for further details.

## Task Management Resources ##

1 of the following 1 resources are expected to have their own API endpoints for GP Connect FoT.

| Resource | Create | Read | Update | Delete | History<br/>Read | Search | Identifier<br/>Search | Bundle<br/>Read | Compartment<br/>Read |  
|----------|--------|------|--------|--------|------------------|--------|-----------------------|-----------------|----------------------|
| [Order](https://www.hl7.org/fhir/DSTU2/order.html) (aka Task) | Yes | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

Refer to [Capability Pack - Task Management](tasks.html) for further details.

{% include links.html %}