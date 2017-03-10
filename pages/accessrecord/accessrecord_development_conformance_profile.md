---
title: Example Conformance Profile
keywords: getcarerecord, development, conformance, metadata
tags: [development,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_development_conformance_profile.html
summary: "Example of a conformance profile for the Access Record capability."
---

## Conformance Statement ##

This is an example of a conformance statement of a GP Connect FHIR server which provides only Access Record HTML Stage 1 capabilities.  See [Get the FHIR Conformance Profile](foundations_use_case_get_the_fhir_conformance_profile.html) for an example showing all capabilities. 

```xml
<Conformance xmlns="http://hl7.org/fhir">
	<version value="1.0.0-rc.1" />
	<name value="GP Connect" />
	<status value="draft" />
	<experimental value="true" />
	<publisher value="NHS Digital" />
	<contact>
		<name value="Software Vendor Contact Name" />
	</contact>
	<date value="2016-08-08" />
	<description value="This server is a reference implementation of the GP Connect FHIR APIs" />
	<copyright value="Copyright NHS Digital 2016" />
	<kind value="capability" />
	<software>
		<name value="Software Name" />
		<version value="Software Verson" />
		<releaseDate value="Software Release Date" />
	</software>
	<fhirVersion value="1.0.2" />
	<acceptUnknown value="both" />
	<format value="application/xml+fhir" />
	<format value="application/json+fhir" />
	<rest>
		<mode value="server" />
		<security>
			<cors value="true" />
			<certificate>
				<blob />
			</certificate>
		</security>
		<resource>
			<type value="Patient" />
			<interaction>
				<code value="read" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="NHS Number (i.e. http://fhir.nhs.net/Id/nhs-number|123456789)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Organization" />
			<interaction>
				<code value="read" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="ODS Code (i.e. http://fhir.nhs.net/Id/ods-organization-code|Y12345) OR ODS Site Code (i.e. http://fhir.nhs.net/Id/ods-site-code|Y12345678)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Practitioner" />
			<interaction>
				<code value="read" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="SDS User Id (i.e. http://fhir.nhs.net/sds-user-id|999999)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Location" />
			<interaction>
				<code value="read" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="ODS Code (i.e. http://fhir.nhs.net/Id/ods-organization-code|Y12345) OR ODS Site Code (i.e. http://fhir.nhs.net/Id/ods-site-code|Y12345678)" />
			</searchParam>
		</resource>
		<operation>
			<name value="Get Care Record" />
			<definition>
				<reference value="OperationDefinition/gpc.getcarerecord" />
			</definition>
		</operation>
	</rest>
	<rest>
		<mode value="server" />
	</rest>
</Conformance>
```

.