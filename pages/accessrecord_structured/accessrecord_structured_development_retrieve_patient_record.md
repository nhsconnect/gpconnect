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

- **MUST** have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
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
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/$gpc.getstructuredrecord
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

The payload request body comprises a `Parameters` resource, conforming to the [GPConnect-GetStructuredRecord-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1) `OperationDefinition` profile.

The `Parameters` resource is populated with the parameters shown below.  Note: The ↳ character indicates a part parameter.

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Optionality</th>
      <th>Cardinality</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="highlighter-rouge">patientNHSNumber</code></td>
      <td><code class="highlighter-rouge">Identifier</code></td>
      <td>Mandatory</td>
      <td>1..1</td>
      <td>NHS Number of the patient for whom to retrieve the structured record.</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeAllergies</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>Include allergies and intolerances in the response.</td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includeResolvedAllergies</code></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Mandatory</td>
      <td>1..1</td>
      <td>
        Include resolved allergies and intolerances in the response.
        <p><i>Part parameter: may only be provided if <code>includeAllergies</code> is set.</i></p>        
      </td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeMedication</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>Include medication in the response.</td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includePrescriptionIssues</code></span></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Mandatory</td>
      <td>1..1</td>
      <td>
        Include each prescription issue in the response.
        <p><i>Part parameter: may only be provided if <code>includeMedication</code> is set.</i></p>        
      </td>
    </tr>
    <tr>
      <td>&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">medicationSearchFromDate</code></td>
      <td><code class="highlighter-rouge">Date</code></td>
      <td>Optional</td>
      <td>0..1</td>
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
    <tr>
      <td><code class="highlighter-rouge">includeConsultations</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>Include consultations in the response.</td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">consultationSearchPeriod</code></span></td>
      <td><code class="highlighter-rouge">Period</code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>
        Restrict consultations by defining a time period

        <ul>
			     <li>If the <code>consultationSearchPeriod</code> is not specified, all consultations will be returned.</li>
			     <li>If the <code>consultationSearchPeriod.start</code> is populated, all consultations on or after the <code>consultationSearchPeriod.start</code> <b>MUST</b> be returned.</li>
           <li>If the <code>consultationSearchPeriod.end</code> is populated, all consultations on or before the <code>consultationSearchPeriod.end</code> <b>MUST</b> be returned.</li>
           <li><code>consultationSearchPeriod.start</code> and <code>consultationSearchPeriod.end</code> <b>MUST</b> be populated with a date less than or equal to the current date.</li>
          <li><code>consultationSearchPeriod.start</code> and <code>consultationSearchPeriod.end</code> <b>MUST</b> be populated with whole dates only (for example, 01-02-2017) - that is, no partial dates, or with a time period or offset.</li>
    	</ul>

        <p><i>Part parameter: may only be provided if <code>includeConsultations</code> is set.</i></p>        
      </td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includeNumberOfMostRecent</code></span></td>
      <td><code class="highlighter-rouge">Integer</code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>
        Limit the number of returned consultations
        <p><i>Part parameter: may only be provided if <code>includeConsultations</code> is set.</i></p>        
      </td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeProblems</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>Include problems in the response.</td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includeStatus</code></span></td>
      <td><code class="highlighter-rouge">Code</code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>
        Restrict the problems that are returned by their clinical status
        <p><i>Part parameter: may only be provided if <code>includeProblems</code> is set.</i></p>        
      </td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includeSignificance</code></span></td>
      <td><code class="highlighter-rouge">Code</code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>
        Restrict the problems that are returned by their clinical significance
        <p><i>Part parameter: may only be provided if <code>includeProblems</code> is set.</i></p>        
      </td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeImmunisations</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>Include immunisations in the response.</td>
    </tr>
    <tr>
      <td><code class="highlighter-rouge">includeUncategorisedData</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>Include uncategorised data in the response.</td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">uncategorisedDataSearchPeriod</code></span></td>
      <td><code class="highlighter-rouge">Period</code></td>
      <td>Optional</td>
      <td>0..1</td>
      <td>
        Restrict uncategorised data by defining a time period

        <ul>
			     <li>If the <code>uncategorisedDataSearchPeriod</code> is not specified, all uncategorised data will be returned.</li>
			     <li>If the <code>uncategorisedDataSearchPeriod.start</code> is populated, all uncategorised data on or after the <code>uncategorisedDataSearchPeriod.start</code> <b>MUST</b> be returned.</li>
           <li>If the <code>uncategorisedDataSearchPeriod.end</code> is populated, all uncategorised data on or before the <code>uncategorisedDataSearchPeriod.end</code> <b>MUST</b> be returned.</li>
           <li><code>uncategorisedDataSearchPeriod.start</code> and <code>uncategorisedDataSearchPeriod.end</code> <b>MUST</b> be populated with a date less than or equal to the current date.</li>
          <li><code>uncategorisedDataSearchPeriod.start</code> and <code>uncategorisedDataSearchPeriod.end</code> <b>MUST</b> be populated with whole dates only (for example, 01-02-2017) - that is, no partial dates, or with a time period or offset.</li>
    	</ul>

        <p><i>Part parameter: may only be provided if <code>includeUncategorisedData</code> is set.</i></p>        
      </td>
    </tr>
  </tbody>
</table>

Each clinical area has its own set of search/filter parameters. These parameters will only apply to their own area and **MUST** have no impact on other parameters.

{% include important.html content="Consumer guidance: The parameters can be used together in a single call or in multiple calls so that information can be retrieved if is required. It is advised that the number of requests that are made to retrieve a patient's record are kept to a minimum." %}

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
          "name": "includePrescriptionIssues",
          "valueBoolean": true
        },
        {
          "name": "medicationSearchFromDate",
          "valueDate": "2017-06-04"
        }
      ]
    },
    {
      "name": "includeConsultations",
      "part": [
        {
          "name": "consultationSearchPeriod",
          "valuePeriod": {
            "start": "2017-12-25",
            "end": "2018-12-25"
          }
        },
        {
          "name": "numberOfMostRecent",
          "valueBoolean": "3"
        }
      ]
    },
    {
      "name": "includeProblems",
      "part": [
        {
          "name": "includeStatus",
          "valueCode": "active"
        },
        {
          "name": "includeSignificance",
          "valueCode": "major"
        }
      ]
    },
    {
      "name": "includeImmunisations"
    },
    {
      "name": "includeUncategorisedData",
      "part": [
        {
          "name": "uncategorisedDataSearchPeriod",
          "valuePeriod": {
            "start": "2016-12-25",
            "end": "2018-12-25"
          }
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
| The provider could not parse the `Parameters` resource.  | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `patientNHSNumber` parameter is not provided | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `patientNHSNumber` parameter value is invalid, for example it fails format or check digit tests | [`INVALID_NHS_NUMBER`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The `medicationSearchFromDate` part parameter contains a partial date, or has a value containing a time or offset component | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `medicationSearchFromDate` part parameter is greater than the current date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeAllergies` parameter is passed without the corresponding `includeResolvedAllergies` part parameter | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeMedication` parameter is passed without the corresponding `includePrescriptionIssue` part parameter | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `consultationSearchPeriod` part parameter is greater than the current date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The end date of the `consultationSearchPeriod` part parameter is greater than the start date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `consultationSearchPeriod` and `includeNumberOfMostRecent` part parameters are both populated  | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `uncategorisedDataSearchPeriod` part parameter is greater than the current date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The end date of the `uncategorisedDataSearchPeriod` part parameter is greater than the start date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeStatus` part parameter contains a value other than `active` or `inactive` | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeSignificance` part parameter contains a value other than `major` or `minor` | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The patient has dissented to sharing their clinical record | [`NO_PATIENT_CONSENT`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| A patient could not be found matching the `patientNHSNumber` provided | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for the record of an [inactive](overview_glossary.html#active-patient) or deceased patient | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for the record of a non-Regular/GMS patient (i.e. the patient’s registered practice is somewhere else) | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The patient's NHS number in the provider system is not associated with a NHS number status indicator code of 'Number present and verified' | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for a sensitive patient | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
|-------------------------|-------------------|

### Forwards and backwards compatibility ###

#### Forwards compatibility ####
Forwards compatibility is the scenario where a consumer requests a higher version of the API than the provider supports. This requires that a provider **MUST** be able to warn a consumer when they don't support a requested parameter.

In this scenario, providers **MUST** respond in the following way:
- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- Include information for supported parameters
- as part of the returned bundle, include an [`OperationOutcome`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) with an `issue` for each unsupported parameter where:
  - `code` = `not-supported`
  - `severity` = `warn`
  - `details.coding` = `NOT_IMPLEMENTED`
  - `details.text` = `<parameter-name> is an unrecognised parameter`

Consumers **MUST** check for the presence of an [`OperationOutcome`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource as described above to check for incomplete data as a result of unsupported parameters.

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
  - `OperationOutcome` containing warnings about any unsupported parameters
  - resources holding consultations, problems, immunisations, allergies, intolerance, medication and uncategorised data according to the rules below:

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

  - and when the `includePrescriptionIssues` parameter is set to `true`:

    - [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) resources with an `intent` of `order` representing the patient's prescription issues, for the above medication summary data

- `Organization`, `Practitioner` and `PractitionerRole` resources that are referenced by the &nbsp; [`MedicationStatement`](accessrecord_structured_development_medicationstatement.html) and &nbsp; [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) resources

<br/>

##### Consultations #####

Provider systems **MUST** include the following in the response `Bundle`:

- when the 'includeConsultations' parameter is not set:

  - no consultation information shall be returned

- when the 'includeConsultations' parameter is set:
  - [`List`](accessrecord_structured_development_list.html), [`Encounter`](accessrecord_structured_development_encounter.html), [`List - Consultation`](accessrecord_structured_development_list_consultation.html) and [`Observation - narrative`](accessrecord_structured_development_guidance_observation_narrative.html) resources representing the patient's consultations
  - and when the `numberOfMostRecent` parameter is set:
    - limit the number of returned consultations to match the included value

- when the 'consultationSearchPeriod' is set:
  - when a `start` value is set, all consultations after the date **MUST** be returned
  - and when an `end` value is set, all consultations before the date **MUST** be returned
  - and when both a `start` and `end` are specified, consultations after the `start` and before the `end` **MUST** be returned


##### Problems #####

Provider systems **MUST** include the following in the response `Bundle`:

- when the 'includeProblems' parameter is not set:

  - no problem information shall be returned

- when the 'includeProblems' parameter is set:

  - [`List`](accessrecord_structured_development_list.html) and [`Condition`](accessrecord_structured_problems.html) resources representing the patient's problems and all linked clinical information.

- and when the 'includeStatus' parameter is set:

  - [`List`](accessrecord_structured_development_list.html) and [`Condition`](accessrecord_structured_problems.html) resources with a `clinicalStatus` matching the parameter value and all linked clinical information.

- and when the 'includeSignificance' parameter is set:

  - [`List`](accessrecord_structured_development_list.html) and [`Condition`](accessrecord_structured_problems.html) resources with a `problemSignificance` matching the parameter value and all linked clinical information


##### Immunisations #####

Provider systems **MUST** include the following in the response `Bundle`:

- when the 'includeImmunisations' parameter is not set:

  - no immunisation information shall be returned

- when the 'includeImmunisations' parameter is set:

  - [`List`](accessrecord_structured_development_list.html) and [`Immunization`](accessrecord_structured_development_immunization.html) resources representing the patient's immunisations will be returned.

##### Uncategorised data #####

Provider systems **MUST** include the following in the response `Bundle`:

- when the 'includeUncategorisedData' parameter is not set:

  - no uncategorised data shall be returned

- when the 'includeUncategorisedData' parameter is set:

  - [`List`](accessrecord_structured_development_list.html) and [`Observation - uncategorised`](accessrecord_structured_development_observation_uncategorisedData.html) resources representing the patient's uncategorised data will be returned.

- when the 'uncategorisedDataSearchPeriod' is set:
  - when a `start` value is set, all uncategorised data after the date **MUST** be returned
  - and when an `end` value is set, all uncategorised data before the date **MUST** be returned
  - and when both a `start` and `end` are specified, uncategorised data after the `start` and before the `end` **MUST** be returned

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

<br/>

#### Bundle population illustrated ####

The following diagram illustrates the population of the response `Bundle` according to the parameters in the inbound `Parameters` request resource:

<img style="max-height: 100%; max-width: 100%" alt="Structured Bundle response" src="images/access_structured/structured-bundle-response.png"/>

#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [Allergies - FHIR examples](accessrecord_structured_development_fhir_examples_allergies.html)
- [Medication - FHIR examples](accessrecord_structured_development_fhir_examples_medication.html)
- [Consultations and problems - FHIR examples](accessrecord_structured_development_fhir_examples_consultations.html)
- [Immunizations - FHIR examples](accessrecord_structured_development_fhir_examples_immunizations.html)
- [Uncategorised data - FHIR examples](accessrecord_structured_development_fhir_examples_uncategorised.html)

To illustrate how forwards compatibility works, the following example has been included:
- [Retrieve consultations, problems, medications and allergies from a provider on version 1.2.3 of the GP Connect API](accessrecord_structured_development_fhir_examples_forwards_consultations.html)
