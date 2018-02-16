---
title: Foundation Resources
keywords: development
sidebar: foundations_sidebar
toc: false
permalink: datalibraryfoundation.html
summary: "The FHIR&reg; profiles and interactions required for the Foundation capability"
---

The following FHIR&reg; resources are used in the current version of the Foundation capabilities, see "API Use Cases" in the menu on the left. Full details of profiled FHIR resources and worked examples are available on the [FHIR Reference Server](https://fhir.nhs.uk/).

## ***[Get the FHIR&reg; conformance profile](foundations_use_case_get_the_fhir_conformance_profile.html)*** ##
### Request ###
N/A - No FHIR resource is sent within the request

### Response ###
* [Conformance](https://www.hl7.org/fhir/DSTU2/conformance.html)

## ***Errors*** ##

If there is a problem with the request or an error occurs during processing of the request then the provider should return a http error along with an "OperationOutcome" Resource within the response payload. Details of the required error responses are available on the [Error Handling Guidance](/development_fhir_error_handling_guidance.html) page within the specification.

### Response ###
* [gpconnect-operationoutcome-1](https://fhir.nhs.uk/StructureDefinition/gpconnect-operationoutcome-1) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html))
