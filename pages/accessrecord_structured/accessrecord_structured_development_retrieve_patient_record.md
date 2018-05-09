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

The payload request body comprises a `Parameters` resource, conforming to the [GPConnect-GetStructuredRecord-Operation-1](accessrecord_structured_development_operation_definition.html) `OperationDefinition` profile.

The `Parameters` resource is populated with the parameters shown below.  Note: The ↳ character indicates a part parameter.

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
      <td>NHS Number of the patient to retrieve the structured record for.</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeAllergies</code></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>Include allergies and intolerances in the response.</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includeResolvedAllergies</code></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>
        Include resolved allergies and intolerances in the response.
        <p><i>Part parameter: may only be provided if <code>includeAllergies</code> is <code>true</code>.</i></p>        
      </td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeMedication</code></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>Include medication in the response.</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">medicationDatePeriod</code></td>
      <td><code class="highlighter-rouge">Period</code></td>
      <td>Optional</td>
      <td>
        Restrict medication returned to that within the date period specified. Rules:
        <ul>
	        <li><code>Period.start</code> and <code>Period.end</code> <b>SHALL</b> be populated with whole dates only (e.g. 01-02-2017), i.e. no partial dates, or with a time period or offset.</li>
	        <li>If the <code>medicationDatePeriod</code> is not specified, all medication will be returned.</li>
	        <li>If <code>Period.start</code> is populated, medication on or after the start date will be returned.</li>
	        <li>If <code>Period.end</code> element is populated, medication on or before the end date will be returned.</li>
	        <li>If <code>Period.start</code> and <code>Period.end</code> are populated, medication between or on the start and end dates will be returned.</li>
    	</ul>
    	<p><i>Part parameter: may only be provided if <code>includeMedication</code> is <code>true</code>.</i></p>
      </td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includePrescriptionIssues</code></span></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>
        Include each prescription issue in the response.
        <p><i>Part parameter: may only be provided if <code>includeMedication</code> is <code>true</code>.</i></p>        
      </td>
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeMedication",
      "part": [
        {
          "name": "medicationDatePeriod",
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

The provider system **SHALL** return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

Errors returned due to parameter failure **MUST** include diagnostic information detailing the invalid parameter.

Errors that may be encountered include:

- the `patientNHSNumber` parameter is not provided
- the `patientNHSNumber` is invalid, for example it fails format or check digit tests
- the `patientNHSNumber` has not been traced or cross-checked on PDS in the providing system
- a patient could not be found matching the `patientNHSNumber` provided
- an invalid `medicationDatePeriod` range is requested (that is, end date < start date)
- `medicationDatePeriod.start` or `medicationDatePeriod.end` contain a partial date, or have a value containing a time or offset component
- the `Parameters` resource passed does not conform to that specified in the [GPConnect-GetStructuredRecord-Operation-1](accessrecord_structured_development_operation_definition.html) `OperationDefinition`
- the provider could not parse, or does not recognise a parameter name or value in the `Parameters` resource

Refer to [Error handling guidance](development_fhir_error_handling_guidance.html) for further information including appropriate error codes.

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

Provider systems **SHALL**:

- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- return a `Bundle` conforming to the [`GPConnect-StructuredRecord-Bundle-1`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1) profile definition
- return the following resources in the `Bundle`:
  - `Patient` matching the NHS Number sent in the body of the request
  - `Organization` matching the patient's registered GP practice, referenced from `Patient.generalPractitioner`
  - `Organization` matching the organisation serving the request, if different from above, referenced from `Patient.managingOrganization`
  - `Practitioner` matching the patient's usual GP, if they have one, referenced from `Patient.generalPractitioner`
  - resources holding allergies and intolerance and medication information according to the rules below:

##### Allergies #####

Provider systems **SHALL** include the following in the response `Bundle`:

- when the `includeAllergies` parameter is not set:

  - no allergy or intolerance information shall be returned

- when the `includeAllergies` parameter is set:

  - and when the `includeResolvedAllergies` parameter is not set or is set to `false`:

    - [`AllergyIntolerance`](accessrecord_structured_development_allergyintolerance.html) resources representing the patient's allergies and intolerances, <i>excluding</i> those marked as resolved or ended

  - and when the `includeResolvedAllergies` parameter is set to `true`:

    - [`AllergyIntolerance`](accessrecord_structured_development_allergyintolerance.html) resources representing the patient's allergies and intolerances, <i>including</i> those marked as resolved or ended

- `Organization`, `Practitioner` and `Location` resources that are referenced by the [`AllergyIntolerance`](accessrecord_structured_development_allergyintolerance.html) resources

<br/>

{% include todo.html content="Allergy list population requirements" %}

##### Medications #####

Provider systems **SHALL** include the following in the response `Bundle`:

- when the `includeMedication` parameter is not set:

  - no medication information shall be returned

- when the `includeMedication` parameter is set:

  - [`MedicationStatement`](accessrecord_structured_development_medicationstatement.html), [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) with an `intent` of `plan` and [`Medication`](accessrecord_structured_development_medication.html) resources representing the patient's medication summary information (authorisations and medication prescribed elsewhere)

  - when the `medicationDatePeriod` parameter is set, the medication summary data **SHALL** be restricted to that whose date falls within, or overlaps (in the case of a range), the `Period.start` and `Period.end`. The date used shall be:

    1 - `effectiveDate` or `effectivePeriod`
      - `effectiveStartDate` - the date the prescription (or cycle of prescriptions) is expected to start. For repeat and repeat dispensed prescriptions this is the period covered by the entire cycle of planned issues
      - `effectiveEndDate` - the date the prescription (or cycle of prescriptions) is expected to finish. For repeat and repeat dispensed prescriptions this is the period covered by the entire cycle of issue. Where this date is not supplied for a repeat dispensed prescription then they are considered ongoing until a date is supplied
    
    2 - `dateAsserted`, where the medication does not have a `lastIssueDate`, `effectiveDate` or `effectivePeriod`

  - and when the `includePrescriptionIssues` parameter is not set, or is set to `false`:

    - no prescription issue information should be returned

  - and when the `includePrescriptionIssues` parameter is set to `true`:

    - [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) resources with an `intent` of `order` representing the patient's prescription issues, for the above medication summary data

- `Organization`, `Practitioner` and `Location` resources that are referenced by the [`MedicationStatement`](accessrecord_structured_development_medicationstatement.html) and [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) resources

<br/>

{% include todo.html content="Medication list population requirements" %}

#### Bundle population illustrated ####

The following diagram illustrates the population of the response `Bundle` according to the parameters in the inbound `Parameters` request resource:

<img style="max-height: 1000px; max-width: 1000px;" alt="Structured Bundle response" src="images/access_structured/structured-bundle-response.png"/>

{% include todo.html content="Update diagram with allergy and medication list population" %}

#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [Allergies - FHIR example 1](accessrecord_structured_development_fhir_examples_1.html)
- [Allergies - FHIR example 2](accessrecord_structured_development_fhir_examples_2.html)
- [Allergies - FHIR example 3](accessrecord_structured_development_fhir_examples_3.html)
- [Medication - FHIR example 4](accessrecord_structured_development_fhir_examples_4.html)

