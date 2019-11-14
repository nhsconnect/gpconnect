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

- **MUST** have previously resolved the organisation's Access Record Structured FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- **MUST** have previously traced the patient's NHS Number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service

## API usage ##

### Interaction diagram ###

<img style="height: 400px;" alt="Get structured record interaction diagram" src="images/access_structured/get-structured-record-interaction-diagram.png"/>

### Request operation ###

#### FHIR&reg; relative request ####

```http
POST /Patient/$gpc.getstructuredrecord
```

#### FHIR&reg; absolute request ####

```http
POST https://[proxy_server]/https://[provider_server]/[structured_fhir_base]/Patient/$gpc.getstructuredrecord
```

#### Request headers ####

Consumers **MUST** include the following additional HTTP request headers:

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

The payload request body comprises a `Parameters` resource, conforming to the [GPConnect-GetStructuredRecord-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1/_history/1.8) `OperationDefinition` profile.

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
      <td>NHS Number of the patient for whom to retrieve the structured record.</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeAllergies</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Optional</td>
      <td>Include allergies and intolerances in the response.</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includeResolvedAllergies</code></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Mandatory</td>
      <td>
        Include resolved allergies and intolerances in the response.
        <p><i>Part parameter: may only be provided if <code>includeAllergies</code> is set.</i></p>        
      </td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeMedication</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Optional</td>
      <td>Include medication in the response.</td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includePrescriptionIssues</code></span></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Optional</td>
      <td>
        Include each prescription issue in the response, this parameter has a default value of 'true'. More guidance relating to its use is available in the <a href="accessrecord_structured_development_medication_guidance.html#medication-search-criteria">Medication guidance page</a>
        <p><i>Part parameter: may only be provided if <code>includeMedication</code> is set.</i></p>        
      </td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">medicationSearchFromDate</code></td>
      <td><code class="highlighter-rouge">Date</code></td>
      <td>Optional</td>
      <td>
        Restrict medications returned on or after the date specified. Rules:
        <ul>
			<li>If the <code>medicationSearchFromDate</code> is not specified, all medication will be returned.</li>
			<li>If the <code>medicationSearchFromDate</code> is populated, all medications which are active on or after the <code>medicationSearchFromDate</code> <b>MUST</b> be returned.</li>
			<li><code>medicationSearchFromDate</code> <b>MUST</b> be populated with a date less than or equal to the current date.</li>
	        <li><code>medicationSearchFromDate</code> <b>MUST</b> be populated with whole dates only (for example, 01-02-2017) - that is, no partial dates, or with a time period or offset.</li>
    	</ul>
    	<p><i>Part parameter: may only be provided if <code>includeMedication</code> is set.</i></p>
      </td>
    </tr>
  </tbody>
</table>

{% include important.html content="Consumer guidance: it is advised that a single call is made to retrieve all structured data required for a patient. In addition, the parameter filters should be applied to reduce the payload." %}

The example below shows a fully populated `Parameters` resource as a request to the `$gpc.getstructuredrecord` operation:

```json
{
  "resourceType": "Parameters",
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
          "name": "medicationSearchFromDate",
          "valueDate": "2017-06-04"
        }
      ]
    }
  ]
}
```

#### Error handling ####

The provider system **MUST** return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shown common errors that may be encountered during this API call, and the returned Spine error code.  Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response, or to determine the response for errors encountered that are not shown below.

Errors returned due to parameter failure **MUST** include diagnostic information detailing the invalid parameter.

|-------------------------|-------------------|
| Error encountered        | Spine error code returned |
|-------------------------|-------------------|
| The `Parameters` resource passed does not conform to that specified in the [GPConnect-GetStructuredRecord-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1) `OperationDefinition` | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| No recognised parameters are provided | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `patientNHSNumber` parameter is not provided | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `patientNHSNumber` parameter value is invalid, for example it fails format or check digit tests | [`INVALID_NHS_NUMBER`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The `medicationSearchFromDate` part parameter contains a partial date, or has a value containing a time or offset component | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `medicationSearchFromDate` part parameter is greater than the current date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeAllergies` parameter is passed without the corresponding `includeResolvedAllergies` part parameter | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The patient has dissented to sharing their clinical record | [`NO_PATIENT_CONSENT`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| A patient could not be found matching the `patientNHSNumber` provided | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for the record of an [inactive](overview_glossary.html#active-patient) or deceased patient | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for the record of a non-Regular/GMS patient (i.e. the patient’s registered practice is somewhere else) | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The patient's NHS number in the provider system is not associated with a NHS number status indicator code of 'Number present and verified' | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for a sensitive patient | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
|-------------------------|-------------------|

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

Provider systems **MUST**:

- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- return a `Bundle` conforming to the [`GPConnect-StructuredRecord-Bundle-1`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1) profile definition
- return the following resources in the `Bundle`:
  - `Patient` matching the NHS Number sent in the body of the request
  - `Organization` matching the patient's registered GP practice, referenced from `Patient.generalPractitioner`
  - `Organization` matching the organisation serving the request, if different from above, referenced from `Patient.managingOrganization`
  - `Practitioner` matching the patient's usual GP, if they have one, referenced from `Patient.generalPractitioner`
  - `PractitionerRole` matching the usual GP's role
  - resources holding allergies, intolerance, medication information and warnings according to the rules below:

Provider systems **SHOULD**:

- provide a consistent order to elements within the `Bundle` resource.  It is recommended to follow the order described in the [Bundle population illustrated](accessrecord_structured_development_retrieve_patient_record.html#bundle-population-illustrated) diagram.

Consumers systems **MUST NOT**:

- rely on order or index of elements within the `Bundle` resource in order to parse encapsulated resources.

##### Allergies #####

Provider systems **MUST** include the following in the response `Bundle`:

- when the `includeAllergies` parameter is not set:

  - no allergy or intolerance information shall be returned

- when the `includeAllergies` parameter is set:

  - and when the `includeResolvedAllergies` parameter is set to `false`:

    - [`List`](accessrecord_structured_development_list.html) and [`AllergyIntolerance`](accessrecord_structured_development_allergyintolerance.html) resources representing the patient's allergies and intolerances, <i>excluding</i> those marked as resolved or ended

  - and when the `includeResolvedAllergies` parameter is set to `true`:

    - [`List`](accessrecord_structured_development_list.html) and [`AllergyIntolerance`](accessrecord_structured_development_allergyintolerance.html) resources representing the patient's allergies and intolerances, <i>including</i> those marked as resolved or ended

- `Organization`, `Practitioner` and `PractitionerRole` resources that are referenced by the &nbsp; [`AllergyIntolerance`](accessrecord_structured_development_allergyintolerance.html) resources

<br/>

##### Medications #####

Provider systems **MUST** include the following in the response `Bundle`:

- when the `includeMedication` parameter is not set:

  - no medication information shall be returned

- when the `includeMedication` parameter is set:

  - [`List`](accessrecord_structured_development_list.html), [`MedicationStatement`](accessrecord_structured_development_medicationstatement.html), [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) with an `intent` of `plan` and &nbsp; [`Medication`](accessrecord_structured_development_medication.html) resources representing the patient's medication summary information (authorisations and medication prescribed elsewhere)

  - when the `medicationSearchFromDate` parameter is set:
	- all medications which are active on or after the `medicationSearchFromDate` **MUST** be returned
	  - A medication is considered active between its `effective.start` and `effective.end` (inclusive)
		  - when a medication **does not** have an `effective.end`:
			- an acute medication is considered active on its `effective.start` only
			- a repeat medication is considered on-going and is active from its `effective.start`
			- when a medication is not defined as an acute or repeat it **MUST** be treated as repeat

  - and when the `includePrescriptionIssues` parameter is set to `false`:

    - no prescription issue information should be returned

  - and when the `includePrescriptionIssues` parameter is set to `true` or not included:

    - [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) resources with an `intent` of `order` representing the patient's prescription issues, for the above medication summary data

- `Organization`, `Practitioner` and `PractitionerRole` resources that are referenced by the &nbsp; [`MedicationStatement`](accessrecord_structured_development_medicationstatement.html) and &nbsp; [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) resources

<br/>


#### Medication search date ####

The `medicationSearchFromDate` identifies the start date of the requested medications search period. An end date cannot be requested by a consumer, so that all searches go to the end of the patient's record.

The scenarios below represent how a selection of acute and repeat medications are returned based on the search date in the request. Each scenario has a different search date. Medications that have been greyed out are not returned in the response.

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a href="#scenario1" data-toggle="tab">Scenario 1</a></li>
    <li><a href="#scenario2" data-toggle="tab">Scenario 2</a></li>
    <li><a href="#scenario3" data-toggle="tab">Scenario 3</a></li>
	<li><a href="#scenario4" data-toggle="tab">Scenario 4</a></li>
</ul>
  <div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="scenario1">
<table class='resource-attributes'>
  <tr>
    <td style="font-size:14px"><b>Search date:</b> <code>15/01/2018</code></td>
	<td style="font-size:14px" align="right"><b>Current date:</b> <code>08/10/2018</code></td>
  </tr>
</table>

{% include image.html file="access_structured/data_filter_scenario1.jpg" url="images/access_structured/data_filter_scenario1.jpg"  max-width="100" caption="click image for full size view" %}
</div>

<div role="tabpanel" class="tab-pane" id="scenario2">
<table class='resource-attributes'>
  <tr>
    <td style="font-size:14px"><b>Search date:</b> <code>01/03/2018</code></td>
	<td style="font-size:14px" align="right"><b>Current date:</b> <code>08/10/2018</code></td>
  </tr>
</table>

{% include image.html file="access_structured/data_filter_scenario2.jpg" url="images/access_structured/data_filter_scenario2.jpg"  max-width="100" caption="click image for full size view" %}
</div>

<div role="tabpanel" class="tab-pane" id="scenario3">
<table class='resource-attributes'>
  <tr>
    <td style="font-size:14px"><b>Search date:</b> <code>08/07/2018</code></td>
	<td style="font-size:14px" align="right"><b>Current date:</b> <code>08/10/2018</code></td>
  </tr>
</table>

{% include image.html file="access_structured/data_filter_scenario3.jpg" url="images/access_structured/data_filter_scenario3.jpg"  max-width="100" caption="click image for full size view" %}
</div>

<div role="tabpanel" class="tab-pane" id="scenario4">
<table class='resource-attributes'>
  <tr>
    <td style="font-size:14px"><b>Search date:</b> <code>08/10/2018</code></td>
	<td style="font-size:14px" align="right"><b>Current date:</b> <code>08/10/2018</code></td>
  </tr>
</table>

{% include image.html file="access_structured/data_filter_scenario4.jpg" url="images/access_structured/data_filter_scenario4.jpg"  max-width="100" caption="click image for full size view" %}
</div>
</div>



#### Bundle population illustrated ####

The following diagram illustrates the population of the response `Bundle` according to the parameters in the inbound `Parameters` request resource:

<img style="max-height: 100%; max-width: 100%" alt="Structured Bundle response" src="images/access_structured/structured-bundle-response.png"/>

#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [Allergies - FHIR examples](accessrecord_structured_development_fhir_examples_allergies.html)
- [Medication - FHIR examples](accessrecord_structured_development_fhir_examples_medication.html)
