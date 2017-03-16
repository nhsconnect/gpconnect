---
title: Access Record HTML Conformance Profile
keywords: getcarerecord, development, conformance, metadata
tags: [development,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_development_conformance_profile.html
summary: "Example of a conformance profile for the Access Record HTML capability."
---

## Conformance Statement ##

This is an example conformance statement for a GP Connect FHIR server which provides only the Access Record HTML Maturity Model Stage 1 capability.

```xml
<Conformance xmlns="http://hl7.org/fhir">
	<version value="1.0.0-rc.5" />
	<name value="Access Record HTML" />
	<status value="draft" />
	<experimental value="true" />
	<publisher value="[Software Vendor Name]" />
	<contact>
		<name value="[Software Vendor Contact Name]" />
	</contact>
	<date value="2016-08-08" />
	<description value="This server implements the GP Connect Access Record HTML FHIR APIs" />
	<copyright value="Copyright NHS Digital 2016" />
	<kind value="capability" />
	<software>
		<name value="[Software Name]" />
		<version value="[Software Verson]" />
		<releaseDate value="[Software Release Date]" />
	</software>
	<fhirVersion value="1.0.2" />
	<acceptUnknown value="both" />
	<format value="application/xml+fhir" />
	<format value="application/json+fhir" />
 	<profile>
 		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-patient-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-practitioner-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-location-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-organization-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-device-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-searchset-bundle-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-carerecord-composition-1"/>
	</profile>
	<rest>
		<mode value="server" />
		<security>
			<cors value="true" />
			<certificate>
				<blob />
			</certificate>
		</security>
		<operation>
			<name value="gpc.getcarerecord" />
			<definition>
				<reference value="OperationDefinition/gpc.getcarerecord" />
			</definition>
		</operation>
	</rest>
</Conformance>
```

Please see [Get the FHIR Conformance Profile](foundations_use_case_get_the_fhir_conformance_profile.html) for an example showing all capabilities. 
