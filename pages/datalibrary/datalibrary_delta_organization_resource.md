---
title: Organization Resource Delta
keywords: development, fhir, resource, organization
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_organization_resource.html
summary: "Organization resource delta between GP Connect and the base FHIR resource."
---
			
Overview of changes made to the standard FHIR&reg; DSTU2 [Organization](https://www.hl7.org/fhir/DSTU2/organization.html){:target="_blank"} resource for use within the GP Connect APIs.

<table>
	<thead>
		<tr>
			<th>Field</th>
			<th>Baseline</th>
			<th>Change</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>	identifier	</td>
			<td>	0..*	</td>
			<td>	0..*	</td>
			<td>	Unique identifier(s) assigned to the Organisation - uses ODS Organisation Code or ODS Site Code	</td>
		</tr>
		<tr>
			<td>	part of	</td>
			<td>	0..1 Reference(Organization)	</td>
			<td>	0..1 Reference(Organization)	</td>
			<td>	The organisation of which this organisation forms a part (for nested organisations) - uses 'gpconnectorganization-1' profile	</td>
		</tr>
</tbody>
</table>			


