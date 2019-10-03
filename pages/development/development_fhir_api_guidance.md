---
title: FHIR&reg; implementation
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_api_guidance.html
summary: "Implementation guidance for developers - focusing on FHIR&reg; specifics"
---

## Purpose ##

This site is intended for use by software developers looking to build a conformant GP Connect API interface using the FHIR&reg; standard, with a particular focus on FHIR specifics.

### Notational conventions ###

The keywords '**MUST**', '**MUST NOT**', '**REQUIRED**', '**SHALL**', '**SHALL NOT**', '**SHOULD**', '**SHOULD NOT**', '**RECOMMENDED**', '**MAY**', and '**OPTIONAL**' on this site are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## FHIR implementation guidance ##

The purpose of the implementation guide is to describe adaptations of the base FHIR specification specific for GP Connect First of Type (FoT) implementations. It therefore focuses mainly on any additional constraints and specialisations from the base specification that apply to GP Connect. The complete specification therefore comprises the base FHIR specification plus the constraints and specialisations described herein. Where there is a conflict between the base specification and this web page, this web page shall take precedence.

### FHIR overview ###

As outlined on the official [HL7&reg; FHIR](http://hl7.org/fhir/STU3/) website:

> FHIR (Fast Health Interoperability Resources) is designed to enable information exchange to support the provision of healthcare in a wide variety of settings. The specification builds on and adapts modern, widely used RESTful practices to enable the provision of integrated healthcare across a wide range of teams and organisations.

### [FHIR timelines](http://hl7.org/fhir/STU3/timelines.html) ###

{% include note.html content="This page is written to accompany the currently released version of FHIR which is **Standard For Trial Use (STU) 3**." %}

STU3 is a pre-release version of FHIR standard and as such is expected to evolve and develop over time. NHS Digital expects FHIR clients and servers (developed as part of GP Connect) to be maintained and uplifted to newer versions of the FHIR&reg; standard as they become available and are staged into the GP Connect programme.

When a new release of the FHIR standard has been published for use NHS Digital will carry out an impact assessment of all FHIR resources used by the GP Connect API project to determine the impact of transitioning to the new FHIR release. Following this assessment, the FHIR resource library will be updated to include resources using this new release. NHS Digital will work with consumers and providers throughout this transition phase and are expected to maintain both versions of the FHIR release until it has been agreed that the old version can be deprecated.

### FHIR implementations ###

The Health Level Seven (HL7&reg;) International standards body maintains a list of open source FHIR implementations on its [Wiki](http://wiki.hl7.org/index.php?title=Open_Source_FHIR_implementations). Currently five FHIR server implementations and a number of client libraries are available as open source software. These are written in a variety of popular programming languages, such as Java, C#.NET, JavaScript and Python.

{% include tip.html content="NHS Digital strongly recommends that software vendors use (and contribute back to) an existing open source FHIR library to both help accelerate development and to grow/mature the open source FHIR ecosystem." %}

### FHIR in scope ###

To help API implementers deal with the FHIR learning curve, NHS Digital has worked to constrain the scope of the FHIR&reg; standard that is expected to be implemented in the first tranche of development work as follows:

1. [Resource](https://www.hl7.org/fhir/STU3/resource.html)
	1. [Resource identity](https://www.hl7.org/fhir/STU3/resource.html#id)
	1. [Business identifiers](https://www.hl7.org/fhir/STU3/resource.html#identifiers)
2. [Domain resource](https://www.hl7.org/fhir/STU3/domainresource.html)
	1. Common API
		1. [Patient](https://www.hl7.org/fhir/STU3/patient.html) profiled as gpconnect-patient-1.
		2. [Practitioner](https://www.hl7.org/fhir/STU3/practitioner.html) profiled as gpconnect-practitioner-1.
		3. [Organisation](https://www.hl7.org/fhir/STU3/organization.html) profiled as gpconnect-organization-1.
		4. [Location](https://www.hl7.org/fhir/STU3/location.html) profiled as gpconnect-location-1
	2. Care record API
		1. Please refer to the [Resource data types](#ResourceDataType) section of this page.
	3. Bookings API
		1. [Schedule](https://www.hl7.org/fhir/STU3/schedule.html) profiled as gpconnect-schedule-1
		2. [Slot](https://www.hl7.org/fhir/STU3/slot.html) profiled as gpconnect-slot-1
		3. [Appointment](https://www.hl7.org/fhir/STU3/appointment.html) profiled as gpconnect-appointment-1
	3. Task API
3. [Resource metadata](https://www.hl7.org/fhir/STU3/resource.html#Meta)
	1. [Profile](https://www.hl7.org/fhir/STU3/resource.html#metadata)
	2. [Version Id](https://www.hl7.org/fhir/STU3/resource.html#metadata)
4. [Bundle](https://www.hl7.org/fhir/STU3/bundle.html)
5. [Data types](https://www.hl7.org/fhir/STU3/datatypes.html)
	1. [Primitive types](https://www.hl7.org/fhir/STU3/datatypes.html#primitive)
		1. All primitive types SHALL be supported.
	2. [Complex types](https://www.hl7.org/fhir/STU3/datatypes.html#complex)
		1. The following complex types SHALL be supported.
			1. [Identifier](https://www.hl7.org/fhir/STU3/datatypes.html#identifier)
			2. [Coding](https://www.hl7.org/fhir/STU3/datatypes.html#codeableconcept)
			2. [Codeable Concept](https://www.hl7.org/fhir/STU3/datatypes.html#coding)
			3. [Period](https://www.hl7.org/fhir/STU3/datatypes.html#period)
		4. It is expected that further complex types will be introduced as required to model structured data.
6. Interactions
	1.  Instance
		1.  [READ](https://www.hl7.org/fhir/STU3/http.html#read)
		2.  [UPDATE](https://www.hl7.org/fhir/STU3/http.html#update)
		3.  [DELETE](https://www.hl7.org/fhir/STU3/http.html#delete)
	2.  Type level
		1.  [CREATE](https://www.hl7.org/fhir/STU3/http.html#create)
		2.  [SEARCH](https://www.hl7.org/fhir/STU3/http.html#search)
7.  [Search](https://www.hl7.org/fhir/STU3/http.html#search)
	1.  [Search parameter types](https://www.hl7.org/fhir/STU3/search.html#ptypes)
		1.  [Date](https://www.hl7.org/fhir/STU3/search.html#date)
		2.  [Token](https://www.hl7.org/fhir/STU3/search.html#token)
		3.  [Reference](https://www.hl7.org/fhir/STU3/search.html#reference)
	2. [Search prefixes](https://www.hl7.org/fhir/STU3/search.html#prefix)
		1. lt (less than)
		2. le (less or equal to)
		3. gt (great than)
		4. ge (greater or equal to)
		5. eq (equal to)
	3.  Parameters for all resources
		1.  [_query](https://www.hl7.org/fhir/STU3/search.html#query)
		2.  [_list](https://www.hl7.org/fhir/STU3/search.html#list)
	4.  Search result parameters
		1.  [_include](https://www.hl7.org/fhir/STU3/search.html#include) can be used internally inside a named `_query` operation.
		2.  [_sort](https://www.hl7.org/fhir/STU3/search.html#sort) can be used internally inside a named `_query` operation.

3.  [Operations](https://www.hl7.org/fhir/STU3/operations.html)
	1.  [Implementation defined operations](https://www.hl7.org/fhir/STU3/operations.html#extensibility)

{% include important.html content="It is fully expected that over time new areas of the FHIR&reg; standard will be brought into scope as new capabilities are requested and vendors' understanding of FHIR&reg; standard matures. This is in line with the agreed iterative/Agile engagement process that has been agreed between the NHS Digital and the principal GP system vendors." %}

### FHIR out of scope ###

GP Connect provider systems are not expected to implement the following aspects of the FHIR&reg; standard under the scope of the first tranche of development work:

1. Operations
	1. Validate a resource
	2. Meta operations
	3. Generate a document
	4. Process message
	5. Find a functional list
	6. ConceptMap operations
	7. Closure table maintenance
	8. Fetch records
	9. Questionnaire operations
	10. Terminology operations
2. Interactions
	1. Instance
		1. HISTORY
		2. [VREAD](https://www.hl7.org/fhir/STU3/http.html#vread)
	2. Type level
		1. HISTORY
	3. Whole system
		1. BATCH TRANSACTION
		2. HISTORY
		3. SEARCH
	4. Conditional interactions
		1. CREATE
		2. UPDATE
		3. DELETE
3. Search
	1. Parameter types
		1. Number
		2. String
		3. Quantity
		4. Composite
		5. URL
	2. Parameters for all resources
		1. _language
		2. _lastUpdate
		3. _tag
		4. _profile
		5. _security
		6. _text
		7. _content
		8. _filter
	3. Search result parameters
		1. _count		
		2. _summary
		3. _elements
		4. _contained
		5. _containedType
	4. Chained parameters
	5. Paging / Page count
4. Resource metadata
	1. lastUpdated
	2. security
	2. tag

{% include warning.html content="Providers are free to implement additional FHIR functionality above that mandated under the GP Connect delivery if they so desire. However, the Spine Secure Proxy (SSP) will only forward accredited system interactions." %}

{% include note.html content="Providers MAY populate meta.lastUpdated (unless stated otherwise in a profile's population guidance) if they hold an accurate date/time associated with the data items making up the profile. Consumers MUST NOT rely on this value being populated." %}

### FHIR system conformance ###

Servers SHALL provide a read-only [FHIR CapabilityStatement resource](https://www.hl7.org/fhir/STU3/capabilitystatement.html) that identifies all the profiles and operations that the server supports for each resource type.

A server's capability statement SHALL be available using the following [capabilities interactions](http://hl7.org/fhir/STU3/http.html#capabilities):

```
GET [base]/metadata {?_format=[mime-type]}
```

Refer to [Foundations - Get The FHIR CapabilityStatement](accessrecord_documents_use_case_get_the_fhir_capability_statement.html) for an example GP Connect FHIR capability statement.

### FHIR resource conformance ###

To help a consumer find the correct set of reports for a use-case, a provider of resources SHALL, for any profile declared in [CapabilityStatement.profile](https://www.hl7.org/fhir/STU3/profiling.html#2.13.0.3.2), mark resources with profile assertions documenting the profile(s) they conform to. A provider of resources SHOULD also ensure that any resource instance that would reasonably be expected to conform to the declared profiles SHOULD be published in this form.

### GP Connect FHIR API conformance ###

GP Connect comprises a number of RESTful API bundles. Each API bundle is intended to support sets of related use cases, for example the Appointment API bundle supports viewing, booking and cancelling GP appointments in a number of scenarios.

Individual API bundles may be provided independently of each other. GP Connect conformance may be claimed in relation to one or more API bundles. A provider claiming to provide an API bundle must be fully conformant (that is, implement all the resource profiles and interactions for the API bundle as specified in this document and all the general requirements described herein).

### Incomplete data - expected behaviour ###

Where resource instance data available in clinical systems is either insufficient or corrupt and thus a resource cannot be constructed by a provider system which meets the associated FHIR profile, the following guidance describes expected behaviour:

**Scenario: GET resource by logical ID**

An HTTP 500 error should be returned with an OperationOutcome resource providing diagnostic details. This may include details of the resource in the location element.

**Scenario: FHIR response bundles**

When a response bundle contains multiple resources, one or more of which cannot be populated as available data does not enable the resource in question to be populated to validate the associated profile, the provider will behave as follows: The request as a whole will error with a 500 HTTP Status returned, together with the appropriate OperationOutcome resource providing diagnostic detail of the error.

## FHIR resources ##

### Resource data types ###
<a name="ResourceDataType"></a>
The FHIR specification defines a set of [data types](https://www.hl7.org/fhir/STU3/datatypes.html) that are used for the resource elements.

The user locale (that is, user's language, region and any special variant preferences that the user may want to see in their user interface) of a system SHALL NOT affect the FHIR on the wire representation of any data types (especially date-time and number formats).

Certain aspects of [primitive data type](https://www.hl7.org/fhir/STU3/datatypes.html#primitive) representation warrant further consideration and SHALL be taken into consideration when designing and constructing FHIR resources.

For example:

- leading 0 digits are not allowed
- strings SHALL NOT exceed 1MB in size
- URIs are case sensitive
- UUID values (urn:uuid:53fefa32-fcbb-4ff8-8a92-55ee120877b7) use all lower case
- dates have no time zone
- dates can be partial dates (for example, just 'year' or 'year + month')
- precision of the decimal value has significance
- primitive types other than string SHALL NOT have leading or trailing whitespace
- [use of null](https://www.hl7.org/fhir/STU3/json.html#null) and empty / zero length values in [XML and JSON representations](https://www.hl7.org/fhir/STU3/datatypes.html#1.19.0.1.1)

### Resource narrative ###

The FHIR [resource narrative](https://www.hl7.org/fhir/STU3/narrative.html) is not currently expected to be populated.

### Resource references ###

The FHIR resource model includes [resource references](http://hl7.org/fhir/STU3/references.html) from one resource to another.

A reference can be either:

- a relative or absolute URL to a resource managed by the same resource server (a local reference), or
- an absolute URL to a resource managed by another resource server (a remote reference)

A provider’s ability to process a request relating to a resource may depend on its ability to utilise one or more resource references that the resource contains (for example, its ability to ‘follow the links’ to other resources).

{% include important.html content="GP Connect clients and servers SHALL use local relative references only and as such the resources will be expected to reside on the same server." %}


### Resource metadata ###

Servers SHALL provide the `profile` [metadata](https://www.hl7.org/fhir/STU3/resource.html#Meta) for each resource, asserting that the content conforms to one of the GP Connect resource profiles.  

Servers SHALL provide the `version Id` metadata for each item. This SHALL change each time the content of the resource changes.

Consumer creating or amending a resource SHALL provide the `profile` metadata details within the sent resource. The `profile` metadata should be checked for by the provider to ensure predictable process and for forward compatibility when a server can handle multiple profiles for the same type of resource.

Clients SHALL use the `version Id` when performing updates to allow [management of resource contention](https://www.hl7.org/fhir/STU3/http.html#concurrency) and to protect against [lost updates](http://www.w3.org/1999/04/Editing/).

### Resource transactions ###

When performing an update or creating [resource transactions](https://www.hl7.org/fhir/STU3/http.html#transactional-integrity), servers:

-	SHALL **validate the content against valid profiles** and business rules before creating/updating the resource
-	MAY apply business rules that alter the content
-	MAY merge updated content with existing content

Servers SHALL validate the existence of any referenced resources when creating or updating a resource. For example, a `Slot` reference (for example, `Slot/D497DB00-99AA-11E5-A837-0800200C9A66`) used when creating a new `Appointment` would be checked for existence on the server and an error returned (and the create interaction aborted) if the slot does not exist.

Refer to the GitHub hosted [GP Connect FHIR repository](https://github.com/nhsconnect/gpconnect-fhir) for the published FHIR profiles.

Refer to the [HL7&reg; FHIR&reg; Validator](https://www.hl7.org/fhir/STU3/validation.html#jar) page for the most up to date details on how FHIR resources can be validated.

Servers SHALL provide a read interaction for every resource it accepts update interactions on.

Consumers SHALL follow the pattern described in the [Transactional Integrity](https://www.hl7.org/fhir/STU3/http.html#transactional-integrity) section of the base FHIR specification, built on top of version-aware updates, for updating resources.

## FHIR&reg; resource interactions ##

### Requests ###

Servers SHALL be able to consume and process the following requests for GP Connect FoT:

| Interaction | Path | Request verb | Request content-type | Body | Prefer | Conditional |
| ----------- | ---- | ------------ | -------------------- | ---- | ------ | ----------- |
| `read`   | `/[type]/[id]` | `GET` | N/A | N/A | N/A | `ETag` |
| `update` | `/[type]/[id]` | `PUT` | R | Resource | O | `If-Match`|
| `delete` | `/[type]/[id]` | `DELETE` | N/A | N/A | N/A | N/A |
| `create` | `/[type]` | `POST` | R | Resource | O | N/A |
| `search` | `/[type]?` | `GET` | N/A | N/A | N/A | N/A |
| `(operation)` | `/[type]/$[name]` `/[type]/[id]/$[name]` | `POST` <br/> `GET` | R <br/> `application/x-www-form-urlencoded` | Parameters <br/> form data | N/A | N/A |

> N/A = not present, R = required, O = optional

### Responses ###

Servers SHALL be expected to produce the following responses for GP Connect FoT:

| Interaction | Response content-type | Body | Location | Content-location | Versioning | Status codes |
| ----------- | --------------------- | ---- | -------- | ---------------- | ---------- | ------------ |
| `read`   | R | R: Resource | N/A | R | `ETag` | `200`, `404`, `410` |
| `update` | R | R: Resource | N/A | R | `ETag` | `200`, `201`, `400`, `404` `405`, `409`, `412`, `422` |
| `delete` | R | R: Operation Outcome | N/A | N/A | N/A | `200`, `204`, `404`, `405`, `409`, `412` |
| `create` | R | R: Resource | R | R | `ETag` | `201`, `400`, `404` `405`, `422` |
| `search` | R | R: Bundle | N/A | N/A | N/A | `200`, `403` |
| `(operation)` | R | R: Parameters/Resource | N/A | N/A | N/A | `200`, `400`, `403`, `404`, `422`  |

> N/A = not present, R = required, O = optional

#### Response codes ####

Servers SHALL produce the following main [HTTP status codes](http://www.iana.org/assignments/http-status-codes/http-status-codes.xhtml):

| HTTP status code | Description |
| ---------------- | ----------- |
| `200` | OK |
| `201` | Created |
| `400` | Bad request |
| `401` | Unauthorized |
| `403` | Forbidden |
| `404` | Not found |
| `405` | Method not allowed |
| `409` | Conflict |
| `410` | Gone |
| `412` | Precondition failed |
| `415` | Unsupported media type |
| `422` | Unprocessable entity |
| `500` | Internal server error |
| `501` | Not implemented |

#### [Rejecting updates](https://www.hl7.org/fhir/STU3/http.html#2.1.0.10.1) ####

[OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html) may be returned with any HTTP `4xx` or `5xx` response, but is not required - many of these errors may be generated by generic server frameworks underlying a FHIR server.

Servers are permitted to reject update interactions because of integrity concerns or other business rules, and return HTTP status codes accordingly (usually a `422`).

As outlined in the FHIR specification, any of these errors SHOULD be accompanied by an [OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html) resource that provides additional detail concerning the issue.

Refer to [FHIR Guidance - Error Handling](development_fhir_error_handling_guidance.html) for full details of error codes that SHALL be used when returning an operation outcome error.

### Compartment based access ###

```
VERB [base]/[compartment_type]/[id]/[type]{?_format=[mime-type]}
```

Each resource type may belong to one or more logical [compartment](http://hl7.org/fhir/STU3/compartmentdefinition.html). A compartment is a logical grouping of resources which share a common property.

Servers SHALL support the `Patient` compartment for `Appointment` access.

The patient compartment includes any resources where the `subject` of the resource is the patient.

For example, to retrieve a list of all a patient's appointments, use the URL:

```http
GET [base]/Patient/[id]/Appointment
```

Servers SHALL support searching within this compartment by `start` and `end` date/time, for example:

```http
GET [base]/Patient/[id]/Appointment?start=[{search_prefix}start_date]{&start=[{search_prefix}end_date]}
```


## Read resource ##

A [resource read](https://www.hl7.org/fhir/STU3/http.html#read) takes the following format:

```http
GET [base]/[type]/[id]{?_format=[mime-type]}
```

The returned resource SHALL have an `id` element with a value that is the [id].

Servers SHALL return an `ETag` header with the `version Id` of the resource.

### Available for resources ###

| Capability   | Resource(s) |
| ------------ | ----------- |
| **Foundations**     | `Patient`, `Practitioner`, `Organization` |
| **Access Record**   | TBC |
| **Appointments**    | `Appointment`, `Schedule`, `Slot`, `Location` |
| **Tasks**           | `Order` |

{% include important.html content="In workshop discussions with all principal GP system vendors it has been agreed that record locking (inside the GP system) will not impact on the ability of clients to query the GP Connect APIs and to obtain the latest saved/committed clinical and administrative data." %}

### Retrieving a patient resource by logical ID ###

#### Request ####

```http
GET [base]/Patient/[id]
```

For example:

```http
GET [base]/Patient/1A6E1B1C-6340-4663-926C-9CD1306EAAF8?_format=application/xml+fhir
```

{% include tip.html content="In this example the response format has been specified in the request URL using the `_format` parameter. This could also have been specified using the HTTP Accept header mechanism." %}

#### Response ####

```xml
<Patient xmlns="http://hl7.org/fhir">
	<id value="1A6E1B1C-6340-4663-926C-9CD1306EAAF8" />
	<meta>
		<profile value="http://fhir.nhs.net/StructureDefinition/gpconnect-patient-1" />
	</meta>
	<identifier>
		<system value="http://fhir.nhs.net/Id/nhs-number" />
		<value value="9900002831" />
	</identifier>
	<identifier>
		<type>
			<coding>
				<system value="http://fhir.nhs.net/ValueSet/gpconnect-patient-identifier-type-1" />
				<code value="Local" />
				<display value="Local identifier" />
			</coding>
		</type>
		<system value="http://fhir.nhs.net/Id/local-identifier" />
		<value value="L12345" />
	</identifier>
	<name>
		<use value="usual" />
		<family value="Taylor" />
		<given value="Sally" />
		<prefix value="Mrs" />
	</name>
	<birthDate value="1947-06-09" />
	<address>
		<use value="home" />
		<type value="both" />
		<line value="42, Grove Street" />
		<city value="Overtown" />
		<district value="West Yorkshire" />
		<postalCode value="LS21 1PF" />
	</address>
</Patient>
```

## Create resource ##

To [create](https://www.hl7.org/fhir/STU3/http.html#create) a new resource a RESTful **POST** operation with a request body SHALL be used.   

```http
POST [base]/[resourcetype]
```

When the server creates a new resource and returns a `201` **Created** HTTP status code, it SHALL also return a `Location` header which contains the new `logical Id` and `version Id` of the created resource.

```http
Location: [base]/[type]/[id]/_history/[vid]
```

[id] and [vid] are the newly created `logical Id` and `version Id` for the resource version. An `ETag` header with the `version Id` and a `Last-Modified` header will also be included in the response.

### Available for resources ###

| Capability   | Resource(s) |
| ------------ | ----------- |
| **Foundations**   | &nbsp; |
| **Access Record** | &nbsp; |
| **Appointments**  | `Appointment` |
| **Tasks**         | `Order` |

{% include important.html content="In workshop discussions with all principal GP system vendors it has been agreed that record locking (inside the GP Community Independence Service (CIS)) will not impact on the ability of clients to query the GP Connect APIs and obtain the latest saved patient data." %}

### Create example: Book an appointment for a patient ###

Refer to [Book an appointment](appointments_use_case_book_an_appointment.html) for request and response body examples for a create request.

## Update resource ##

To [update](https://www.hl7.org/fhir/STU3/http.html#update) an existing resource, a RESTful **PUT** operation with a request body SHALL be used.

```http
PUT [base]/[resourcetype]/[id]
```

The PUT operation will only be used to update existing resources. If the specified resource within the URL does not exist on the provider system an error SHALL be returned.

| Capability       | Resource(s) | Field(s) |
| ------------ | ----------- | -------- |
| **Foundations**   | &nbsp; | &nbsp; |
| **Access Record** | &nbsp; | &nbsp; |
| **Appointments**  | `Appointment` | reason, description, comment |
| **Tasks**         | &nbsp; | &nbsp; |

### Update example: Modify the appointment booking reason ###

Refer to [Amend an appointment](appointments_use_case_amend_an_appointment.html) for request and response body examples for a request which updates a resource using the PUT HTTP verb.

## Delete resource ##

To [delete](https://www.hl7.org/fhir/STU3/http.html#delete) an existing resource, a RESTful **DELETE** operation with no request body SHALL be used.

```http
DELETE [base]/[resourcetype]/[id]
```

| Capability   | Resource(s) |
| ------------ | ----------- |
| **Foundations**   | &nbsp; |
| **Access Record** | &nbsp; |
| **Appointments**  | &nbsp; |
| **Tasks**         | &nbsp; |

{% include important.html content="GP Connect clients and servers are currently not expected to utilise the ability to delete a resource using the RESTful DELETE operation. However, this section is included as implementers should ensure that their implementation choices don't preclude the use of this HTTP verb in future release." %}

## Operations ##

[Operations](https://www.hl7.org/fhir/STU3/operations.html) are used (a) where the server needs to play an active role in formulating the content of the response, not merely return existing information, or (b) where the intended purpose is to cause side effects such as the modification of existing resources, or creation of new resources.

As outlined in the [Extend and Restricting the API](https://www.hl7.org/fhir/STU3/profiling.html#api) section of the FHIR&reg; standard,  NHS Digital has decided to prefix its operation names with a short prefix (for example, `gpc`) followed by a '.' to reduce the likelihood of name conflicts.

## Search resources ##

A simple [search](https://www.hl7.org/fhir/STU3/http.html#search) is executed by performing a `GET` request optionally accompanied by zero or more name-value URL encoded parameters:

```http
GET [base]/[resourcetype]?name=value&...
```

In order to enable searching by date/time range, servers SHALL support the following prefixes as defined in the base FHIR specification for date parameters: eq, gt, lt, ge, le.

To search for all the appointments for a patient that occurred over a 2-year period:

```http
GET [base]/Patient/1A6E1B1C-6340-4663-926C-9CD1306EAAF8/Appointment?start=ge2014-01-01&start=le2015-12-31
```

### Chained parameters ###

Servers SHALL support searching by a [chained](https://www.hl7.org/fhir/STU3/search.html#2.1.1.4.13) `Patient` identifier parameter for references to `Patient` resources that conform to the `GP-Patient` profile (and therefore have an NHS number identifier). For example:

```http
GET [base]/AllergyIntolerance?patient.identifier=http://fhir.nhs.net/Id/nhs-number|1234569876
```

{% include important.html content="GP Connect clients and servers are not expected to support arbitrary ad hoc searching." %}

### Search example: Search for a patient resource by business ID ###

#### Request ####

```http
GET [base]/Patient?identifier=http://fhir.nhs.net/Id/nhs-number|9900002831
```

If a patient resource for NHS number 9900002831 exists then the server SHALL return a bundle containing all patient resources with the specified NHS number identifier.

#### Response ####

```xml
<Bundle>
	<Patient xmlns="http://hl7.org/fhir">
		<id value="1A6E1B1C-6340-4663-926C-9CD1306EAAF8" />
		<meta>
			<profile value="http://fhir.nhs.net/StructureDefinition/gpconnect-patient-1" />
		</meta>
		<identifier>
			<system value="http://fhir.nhs.net/Id/nhs-number" />
			<value value="9900002831" />
		</identifier>
		<name>
			<use value="usual" />
			<family value="Smith" />
			<given value="Mike" />
			<prefix value="Mr" />
		</name>
		<birthDate value="1977-01-09" />
		<address>
			<use value="home" />
			<type value="both" />
			<line value="2, The Green" />
			<city value="Harrogate" />
			<district value="Yorkshire" />
			<postalCode value="HG1 4AF" />
		</address>
	</Patient>
</Bundle>
```

### Advanced search ###

Servers SHALL implement the [_query](https://www.hl7.org/fhir/STU3/search.html#query) search parameter to enable custom-named search profiles to be defined and used which describe a specific query operation.

```http
GET [base]/[resourcetype]?_query=[query_name]&name=value&...
```

Servers SHOULD implement the standard search equivalent of the advanced custom-named search for queries defined under the GP Connect FoT.

#### Request ####

```http
GET [base]/Schedule?_query=getschedule&date=ge2016-05-12&date=le2016-05-26
```

#### Response ####

```xml
<Bundle xmlns="http://hl7.org/fhir">
	 <type value="searchset"/>
</Bundle>
```
