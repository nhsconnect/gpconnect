---
title: Stage 1. Test Window
keywords: development testing
tags: [development,testing]
sidebar: overview_sidebar
permalink: development_stage_one_test_window.html
summary: "Details of what we're proposing to test in the stage one test window"
---

## Purpose ##

This page is intend to set-out in simple terms what is required for successful participation in the GP Connect *Stage 1. Test Window*. The business capabilities to be tested include HTML get care record, Appointment & Task management.

## Test Strategy ##

Testing is intended to be self-directed with support from NHS Digital staff members when required. GP Principal system vendors are welcome to undertake both consumer and provider roles and explore any/all RESTful API interactions which are in-scope for GP Connect FoT. However, it is expected that all consumer to provider API interactions will be made via the Spine Security Proxy (SSP) and as such all communications will be secure and audited.

![Spine Security Proxy Block Diagram](images/integration/Spine Security Proxy Block Diagram.png)

### Testing Scope ###

NHS Digital suggests that the following business capabilities (depending on availability) would be a reasonable starting point for exploratory testing purpose.

- Integration with the Spine Security Proxy
- Demonstration of some end-to-end interconnectivity and business capabilities
	- HTML Get Care Record Views (with minimal Bundled Structured)
	- Appointment and Task management

{% include important.html content="In this the first GP Connect test window no testing is expected to take place between different GP Principal systems as this is with-in the scope of the second GP Connect test window." %}

### Test Environment ###

As testing is to be adhoc and focused predominantly on proving end-to-end connectivity all testing is expected to be performed in the NHS Digital DEV environment.

GP Principal system vendors are already setup to access this environment (i.e. with the correct firewall rules) and have access to previously issued PKI certificates and endpoint records in SDS. Hence, for GP Connect testing these existing assets are expected to be leveraged.

NHS Digital will undertake the registration of new `InteractionID` and Endpoint records in SDS for the purpose of end to end testing. 

> Note: as previously advised in the NHS Digital workshops the GP Principal system vendors will need to undertake some limited development and configuration work to enable successful communication with the Spine Security Proxy (please refer to the later sections of this document for details).

### Test Data ###

GP Principal system vendors can utilise their existing PDS test patients in the DEV environment. If additional test data is required, this can be made available on request to the SA Functional Assurance mailbox.

## Integration Points ##

### Existing ###

The following existing integration prerequisites are expected of the GP Principal systems:

- PKI certificates (Spine issued)
- PDS (or SMSP) integration<sup>^</sup>
- SDS integration<sup>^</sup>

<sup>^</sup> whilst demonstration of integration with PDS and SDS is desirable, it can be avoid in the first instance by manual configuration of ACID and Endpoint details.

### New ###

The following new integration prerequisite is expected of the GP Principal systems:

- SSP integration

#### Spine Security Proxy Integration ####

> Note: full details of the SSP's operation and the integration responsibilities of both consumer and provider can be found in the [Spine Security Proxy Implementation Guide](integration_spine_security_proxy_implementation_guide.html).

Whilst it is desirable that consumers and providers validate NHS Number's against test patient records in the PDS service this is not a mandatory requirement for successfully completion of this phase of testing.

{% include tip.html content="If a GP Principal system is capable of undertaking both a consumer and provider role then it's acceptable to set the `Ssp-From` and `Ssp-To` headers to the same `ASID` value. Furthermore, as the URL endpoint information is known this can also be locally configured to avoid the need for SDS integrate at this stage." %}

## System Responsibilities ##

As a minimum the following responsibilities should be implemented:

### Consumer ###

- Provides PKI client credentials to allow verification of consumer system by the proxy system.
- Validation by the consumer of PKI server credentials to allow verification of proxy system.
- Addition of Spine HTTP headers to allow secure routing & system-level auditing.
	- `Ssp-TraceID`
		- `GUID/UUID` which identifies the sender's message/interaction (to be generated per request).
	- `Ssp-From`
		- `ASID` which identifies the sender's FHIR endpoint.
	- `Ssp-To`
		- `ASID` which identifies the recipient's FHIR endpoint.
	- `Ssp-InteractionID`
		- `InteractionID` of the operation being performed.
- Construction of URL formatted for valid consumption by the proxy system.
	- `https://[proxy_server]/https://[provider_server]/[fhir_base]/[fhir_request]`
- Correct handling of successful/failed/rejected requests in-line with the HTTP standard.
	- `200` OK.
	- `4xx` and `5xx` HTTP error codes.

A table of `InteractionIDs` can be found in *InteractionIDs for GP Connect* the appropriate interaction identifier is expected to be provided (in the `Ssp-InteractionID` HTTP header) along with the RESTful API call it relates too.

> For the DEV environment `[proxy_server]` = *msg.dev.spine2.ncrs.nhs.uk*

### Provider ###
 
- Provides PKI server credentials to allow verification of provider system by the proxy system.
- Validation by the provider of PKI credentials to allow verification of proxy system.
- Processing of FHIR conformant API requests and generation of FHIR conformant responses.
- Error response generation in line with FHIR and HTTP standards.
	- `200` OK.
	- `4xx` and `5xx` HTTP error codes.

{% include warning.html content="Before forwarding a request to a provider system the SSP will perform both PKI and `ASID`/`InteractionID` related security checks against the consumer system rejecting the request as `403` **Forbidden** if appropriate." %}

## Testing Approach ##

Once successful SSP integration has been achieved testing will commence utilising RESTful APIs in-line with the FHIR&reg; standard and the previously published "GP Connect - FHIR Implementation Guide".

GP Principal vendors are expected to have developed suitable consumer PoC test script(s) to demonstrate end to end integration.

{% include tip.html content="This could be as simple as a set of CURL commands executed at the command line or a set of discrete code snippets (run using a tool like LinqPad) to exercise individual RESTful APIs." %}

## InteractionIDs for GP Connect ##

All `InteractionIDs` are expected to follow the following format `urn:nhs:names:services:[program]:[standard]:[mechanism]:[operation]:[subject]`.

{% include note.html content="`InteractionIDs` are to be considered case-sensitive." %}

- Program = `gpconnet`
- Standard = `fhir`
- Mechanism = [ `rest`, `operation` ]
	- `rest` for RESTful API Interactions.
	- `operation` for custom Operation API Interactions.
- Operation
	- RESTful syle API = [ `create`, `read`, `update`, `delete`, `search` ] + any more specific actions (i.e. `cancel`).
	- RPC style API = [ `gpc.getcarerecord`, `gpc.getschedule`, `gpc.registerpatient` ]
- Subject = [ `resourceType`, `operationName` ]
	- Resource Type is the name of a FHIR resource (i.e. `Patient`, `Appointment`, `Organization` etc).
	- Operation Name is the name of a custom FHIR operation (i.e. `gpc.getcarerecord`)

| Operation                 | InteractionID             | Http Verb | Example URL Pattern |
|---------------------------|---------------------------| ----------|---------------------|
| Read Metadata             | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata` | `GET`  | `[base]/metadata` |
| Read Patient              | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient` | `GET`  | `[base]/Patient/[id]` |
| Patient Search            | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient` | `GET`  | <code>[base]/Patient?identifier=[nhsNumber]&#124;http://fhir.nhs.net/Id/nhs-number</code> |
| Read Practitioner        | `urn:nhs:names:services:gpconnect:fhir:rest:read:practitioner` | `GET`  | `[base]/Practitioner/[id]` |
| Practitioner Search       | `urn:nhs:names:services:gpconnect:fhir:rest:search:practitioner` | `GET`  | <code>[base]/Practitioner?identifier=[sdsUserID]&#124;http://fhir.nhs.net/Id/sds-user-id</code> |
| Read Organisation         | `urn:nhs:names:services:gpconnect:fhir:rest:read:organization` | `GET`  | `[base]/Organization/[id]` |
| Organisation Search       | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization` | `GET`  | <code>[base]/Organization?identifier=[odsCode]&#124;http://fhir.nhs.net/Id/ods-organization-code</code> |
| Read Location             | `urn:nhs:names:services:gpconnect:fhir:rest:read:location` | `GET`  | `[base]/Location/[id]` |
| Location Search           | `urn:nhs:names:services:gpconnect:fhir:rest:search:location` | `GET`  | <code>[base]/Location?identifier=[odsSiteCode]&#124;http://fhir.nhs.net/Id/ods-site-code</code> <br/>&nbsp;<br/> <code>[base]/Location?identifier=[odsCode]&#124;http://fhir.nhs.net/Id/ods-organization-code</code> |
| Get Care Record           | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord` | `POST` | `[base]/Patient/$gpc.getcarerecord` |
| Get Organisation Schedule | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getschedule` | `POST` | `[base]/Organization/[id]/$gpc.getschedule` |
| Read Appointment          | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment` | `GET`  | `[base]/Appointment/[id]` |
| Create Appointment        | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment` | `POST` | `[base]/Appointment` |
| Amend Appointment         | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` | `PUT`  | `[base]/Appointment/[id]` |
| Cancel Appointment        | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` | `PUT`  | `[base]/Appointment/[id]` |
| Create Task               | `urn:nhs:names:services:gpconnect:fhir:rest:create:order` | `POST` | `[base]/Order` |
| Get Patient Appointments  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments` | `GET`  | `[base]/Patient/[id]/Appointment` |
| Register Patient          | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient` | `POST`  | `[base]/Patient/$gpc.registerpatient` |