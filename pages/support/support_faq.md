---
title: Frequently Asked Questions (FAQ)
keywords: support, faq, questions
tags: [support]
toc: false
sidebar: overview_sidebar
permalink: support_faq.html
summary: "Frequently Asked Questions (FAQ) related to the GP Connect technical specification."
---

#### Why is the technical barrier to entry to GP Connect quite high? ####

We're keen to deliver something that we can work with in an open and collaborative way quickly and safely that can be improved over time. This has meant that for 'first of type' we've borrowed some capabilities and governance from other central services such as the PDS look-up service (e.g. PDS compliant system or SMSP client), and ODS lookup service (for end point lookup).

This can be understandable frustrating as a consumer that does not already have access to these prerequisites on day one so we're working hard in the near future to wrap these capabilities within the same GP Connect offering.

#### It is not clear which parts of the FHIR standard are not in scope for the GP Connect programme. ####

Please refer to the [FHIR Out Of Scope](development_fhir_api_guidance.html#fhir-out-of-scope) section for details on what parts of the FHIR standard are currently considered out of scope.

#### Why are you not using the latest version of FHIR (DSTU3)? ####

As DSTU3 hasn’t yet been balloted the current version of FHIR is still DSTU2 and will be until later this year or early next year. Grahame Grieve has recently posted an update on his [OnFHIR blog](https://onfhir.hl7.org) around the next version of FHIR being a STU3 release with a tentative target release date of December 31st 2016.

As outlined in the [FHIR Timelines](development_fhir_api_guidance.html#fhir-timelineshttphl7orgfhirtimelineshtml) section uplifting to newer versions of the FHIR standard is expected (in the sense that in principle it shouldn’t come as a surprise to anyone, as we’re utilising what is currently still a draft standard after all). The mechanism and timing of uplifts will be agreed as part of the commercial CCN conversations.

#### Why are you mandating support for both XML and JSON formats? ####

Both JSON and XML serialisation formats are in scope for a number of reasons. After surveying the existing major FHIR implementations they almost all support both JSON and XML. As a FHIR back-end service it is important to enable ‘low impedance’ integration with both traditional server/desktop applications (which often use XML) and mobile/web applications (which are largely JSON). Obviously, when establishing a new open API ecosystem we want to be as open and inclusive as possible and hence feel that excluding either format would be a divisive move. 
Several existing open source FHIR libraries exist which already supports both serialization formats (such as Java HAPI or Furore FHIR .NET) which should minimise development overhead for implementers.

To ensure maximum accessibility, GP Connect is expecting producers to support both formats. However since XML is on average 30% larger on the wire there is a preference towards use of JSON.

#### Why does the specification include CRUD interactions especially DELETE when not needed? ####

The [Delete Resource](development_fhir_api_guidance.html#delete-resourcehttpswwwhl7orgfhirdstu2httphtmldelete) section is included for completeness to illustrate how a RESTful API (such as FHIR) is designed to support the basic Create, Update and Delete (CRUD) operations. It is made clear in this section that GP Connect FoT clients and servers are not expected to implement this operation at this stage but shouldn’t make implementation decisions that preclude the use of the DELETE HTTP verb in the future.
It may be the case that the DELETE verb is used in future incarnations of GP Connect.  However the effect of these on the target systems may be a “soft” delete.

#### Why does the specification mandate support for FHIR functionality that may not be necessary for GP Connect? ####

In writing the FHIR implementation guidance for GP Connect we have worked hard to cut down the scope of the FHIR standard that needs to be considered when implementing the first tranche of development work. The “FHIR Out Of Scope” section was included to be as explicit as possible what FHIR functionality we don’t need at this stage. However, as with all standards there is a minimal viable subset which we should be looking to support.

#### Why is the Task resource in DSTU3 not being used rather than overloading the Order resource which is a less than perfect fit for tasks? ####

Please see the answer above re: timeframes for the FHIR STU3 release.

#### Why is support built in for accessing specific resources when the requirement is for the record for a specified patient? ####

As outlined in the [Compartment Based Access](development_fhir_api_guidance.html#compartment-based-accesshttphl7orgfhircompartmentshtml) section the scope of the Patient Compartment in the GP Connect FoT is limited to Appointment access only. Conceptually, any and all resources where the subject of the resource is a patient could be made available, however this isn’t mandated.

#### Why does the guidance include support for amendment to appointments? ####

In one of the workshops there was a discussion around appointment updates being problematic and we did discuss putting them out of scope. However, after wider stakeholder review it was decided that we should look at limiting the scope of updates (rather than removing the requirement all together). Hence, we have decided to allow updating a small subset of fields on the appointment (i.e. appointment reason/description). We feel this strikes the right balance between allowing minor corrections to be made whilst avoiding the added complexity of some update use cases; particularly rescheduling which can arguably be more easily handled by a cancel operation followed by the creation of a new appointment.

#### Why is resource versioning included as a mandatory requirement? ####

It is a key principle of the FHIR RESTful APIs that all resources are versioned; without this support no updates to data can ever be safely performed. This is explained in the “Lost Updates” section and “Transactional Integrity” sections of the FHIR standard. Whilst we recognise that it is not necessary to persist versioned access to historical records, it is important that the latest record version can be ascertained. David Hay (Product Strategist at Orion Health) has a blog post on how systems that don’t fully support versions can handle this requirement in a simple and straight forward way.

[https://fhirblog.com/2013/11/21/fhir-versioning-with-a-non-version-capable-back-end/](https://fhirblog.com/2013/11/21/fhir-versioning-with-a-non-version-capable-back-end/)

#### Will it be necessary in all cases to use an NHS service to look up staff/organisation/location information when a supplier may have their own index of this information? ####

You are welcome to use your own ODS index (i.e. to find an organisation by name/address etc.). However, you will need to perform an SDS lookup using the ODS code to resolve the FHIR endpoint that represents that ODS code for the purpose of exposing the Access Record, Appointment and Task APIs.

#### It will be necessary in some use cases to support a search on GMC or NMC number rather than SDS User Id to find a staff member. ####

This has been added to our known issue list so we can provide more guidance on how this could work. However, it is important to note that the [Find A Practitioner](foundations_use_case_find_a_practitioner.html) section gives an example of using a SDS User Id but the same API call could in fact also be used to search by other identifiers by changing the ‘system’ component of the search parameter.

#### Why does the specification support sending tasks to an individual staff member? ####

This information was incorrect in early versions of the API implementation guide and has now been amended. Tasks will only be sent to an organisation not an individual.

#### Why does the guide suggest that all resources should include text in the display property when this information is also in the HTML view? ####

The display property is relevant to the Appointment and Task APIs not the HTML view. More guidance on the use of the display property has been requested by a vendor to facilitate streamlined display of the structured data.

#### Why is oAuth2 not used? ####

Authentication will be via mutual TLS/SSL authentication. The JWT web token has been proposed to allow the easy bundling of related authentication details and to eliminate the need for many separate customer headers, or a bespoke GP Connect bundling format to be defined, implemented and maintained.

#### Why are JSON Web Tokens (JWT) required? ####

Extra HTTP headers are needed for sending provenance/audit details. Sending this data in a JWT Bearer token (which is simply a fragment of JSON) is an easy way of achieving the communication of this data and various libraries exist to make authoring this content trivial.

#### Why is NHS Number not being used as the actual Id for the Patient resource? ####

As outlined in the FHIR standard there is a clear demarcation between business identifiers (such as NHS number, CHI number etc.) and logical identifiers which are opaque and only guaranteed to be valid on the FHIR server they are served from.
 
FHIR’s logical ids are strings which meet the following regex [A-Za-z0-9\-\.]{1,64} (in the reference implementations) logical id’s are often the physical record identity (i.e. a database primary key or a document store guid). So whilst technically a vendor could use the NHS number as their logical ids (as it would match the regex above) this won’t be mandated and can’t be relied upon by consumer applications, which will need to resolve the logical id from the business id.
 
This approach is consistent with the FHIR reference implementations and commercial offerings and is in line with what the wider code4health community is asking for.

#### Why is there to be a centrally-held list of error codes in addition to the standard HTTP response codes? ####

The list of error codes is really intended to allow consumer applications to make sense of errors that the human operator could potentially do something about. We recognise there is a cost-benefit trade-off in this space and will look to only introduce error codes (above that of the base FHIR specification) when they add sufficient value. For example a 400 - Bad Request error code in isolation doesn’t help you determine which input parameter(s) are malformed and similarly a 422 -  Unprocessable Entity doesn’t in isolation help you determine which business rule (or integrity constraint) has caused an operation to fail. 

Defining a small number of supplementary error codes to be included in the Operation Outcome entity allows sense to be made of these failing interactions (i.e. you’ve requested an Appointment to be booked into a slot that is already Busy).

