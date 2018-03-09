---
title: Retrieve a patient's structured record
keywords: getstructuredrecord, view
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_retrieve_patient_record.html
summary: "Retrieve a patient's record in structured format"
---

## Use case ##

Retrieve a patient's record in FHIR&reg; structured format from a GP practice.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details 

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- **SHALL** have previously traced the patient's NHS Number using the [Personal Demographics Service](https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service

## API usage ##

### Request operation ###

#### FHIR&reg; relative request ####

```http
POST /Patient/$gpc.getstructuredrecord
```

#### FHIR&reg; absolute request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/$gpc.getstructuredrecord
```

#### Request headers ####

Consumers **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's Trace ID (a GUID or UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getstructuredrecord-1`|

Example HTTP request headers:

```http
Accept: application/fhir+json;charset=utf-8
Content-Type: application/fhir+json;charset=utf-8
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:operation:gpc.getstructuredrecord-1
```

#### Payload request body ####

The payload request body is a `Parameters` resource, conforming to the [GPConnect-GetStructuredRecord-Operation-1](accessrecord_structured_development_operation_definition.html) `OperationDefinition` profile.

The `Parameters` resource is populated with the following parameters for this operation:

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Optionality</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="highlighter-rouge">patientNHSNumber</code></td>
      <td><code class="highlighter-rouge">Identifier</code></td>
      <td>Mandatory</td>
      <td>NHS number of the patient to retrieve the structured record for</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeAllergies</code></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>Include allergies and intolerances in the response</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includeEndedAllergies</code></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>Include ended allergies and intolerances in the response</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeMedication</code></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>Include medication in the response</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">medicationTimePeriod</code></td>
      <td><code class="highlighter-rouge">Period</code></td>
      <td>Optional</td>
      <td>
        Restrict medication returned to that within the time period specified.
        <p>If no time period is specified, all medication will be returned.</p>
        <p>If the start element is populated, medication on or after the start date will be returned.</p>
        <p>If the end element is populated, medication before on or after the start date will be returned.</p>
        <p>If the start and end elements are populated, medication between or on the start and end date will be returned.</p>
      </td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includePrescriptionIssues</code></span></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>Include each prescription issue in the response</td>
    </tr>
  </tbody>
</table>


{% include important.html content="Consumer guidance: it is advised that a single call is made to retrieve all structured data required for a patient. In addition, the parameter filters should be applied to reduce the payload." %}

The example below shows a fully populated `Parameters` resource as a request to the `$gpc.getstructuredrecord` operation:

```json
{
  "meta": {
    "profile": {
      "value": "https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1"
    }
  },
  "parameter": [
    {
      "name": "patientNHSNumber",
      "valueIdentifier": {
        "system": "https://fhir.nhs.uk/Id/nhs-number",
        "value": "9999999999"
      }
    },
    {
      "name": "includeAllergies",
      "part": [
        {
          "name": "includeEndedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeMedication",
      "part": [
        {
          "name": "medicationTimePeriod",
          "valuePeriod": {
            "start": "2017-01-01",
            "end": "2018-02-01"
          }
        },
        {
          "name": "includePrescriptionIssues",
          "valueBoolean": true
        }
      ]
    }
  ]
}
```

#### Error handling ####

The provider system **SHALL** return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

Errors that may be encountered include:

- the `patientNHSNumber` parameter is not provided
- the `patientNHSNumber` is invalid, for example it fails format or check digit tests
- the `patientNHSNumber` has not been traced or cross checked on PDS in the providing system
- no patient could be found matching the `patientNHSNumber` provided
- an invalid `timePeriod` is requested (that is, end date > start date)
- the provider could not parse, or does not recognise a parameter in the `Parameters` resource

Refer to [Error handling guidance](development_fhir_error_handling_guidance.html) for further information including appropriate error codes.

{% include important.html content="Provider systems **SHOULD** return informative messages if an error occurs." %}

### Request response ###

#### Response headers ####

```http
HTTP/1.1 200 OK
Cache-Control: no-store
Content-Type: application/json+fhir; charset=utf-8
Date: Sun, 07 Aug 2016 11:13:05 GMT
Content-Length: 1464
```

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- **SHALL** return a `Bundle` conforming to the [`GPConnect-GetStructured-Bundle-1`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-GetStructuredRecord-Bundle-1) profile definition
- **SHALL** always return the following resources:
  - `Patient` matching the NHS number sent in the body of the request
  - `Organization` matching the patient's registered GP practice, referenced from `Patient.generalPractitioner`
  - `Organization` matching the organisation serving the request (if different from above), referenced from `Patient.managingOrganization`
  - `Practitioner` matching the patient's registered GP practice, referenced from `Patient.generalPractitioner`

<br/>

The following diagram illustrates the response `Bundle` and resources returned within it returned:

![Structured Bundle response](images/access_structured/structured-bundle-response.png)

#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [FHIR example 1](accessrecord_structured_development_fhir_examples_1.html)
- [FHIR example 2](accessrecord_structured_development_fhir_examples_2.html)
- [FHIR example 3](accessrecord_structured_development_fhir_examples_3.html)

