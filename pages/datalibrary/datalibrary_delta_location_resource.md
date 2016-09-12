---
title: Location Resource Delta
keywords: development, fhir, resource, location
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_location_resource.html
summary: "Location resource delta between GP Connect and the base FHIR resource."
---

Overview of changes made to the standard FHIR&reg; DSTU2 [Location](https://www.hl7.org/fhir/DSTU2/location.html){:target="_blank"} resource to allow its usage within the GP Connect APIs.

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
			<td>	Unique code assigned to the location. - uses ODS Site Code or Other Identifier	</td>
		</tr>
		<tr>
			<td>	name	</td>
			<td>	0..1	</td>
			<td>	1..1	</td>
			<td>	Name of location.	</td>
		</tr>
		<tr>
			<td>	mode	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	Not defined in current profile, however this may be added and required in a future release.	</td>
		</tr>
		<tr>
			<td>	physicalType	</td>
			<td>	0..1	</td>
			<td>	0..1	</td>
			<td>	Type of location in physical form.	 - uses 'CDA Care Setting Type SnCT' valueset and includes READ V2 and CTV3 coding options</td>
		</tr>
		<tr>
			<td>	position	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	Not currently defined in current profile, however this may be added and required in a future release.	</td>
		</tr>
		<tr>
			<td>	managingOrganization	</td>
			<td>	0..1 Reference(Organization)	</td>
			<td>	0..1 Reference(Organization)	</td>
			<td>	Organisation managing the location.	- uses 'gpconnectorganization-1' profile</td>
		</tr>
		<tr>
			<td>	partOf 	</td>
			<td>	0..1 Reference(Location)	</td>
			<td>	0..1 Reference(Location)	</td>
			<td>	Organisation the location forms part of - uses 'gpconnectlocation-1' profile	</td>
		</tr>
	</tbody>
</table>


{% include links.html %}