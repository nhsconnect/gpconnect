---
title: Practitioner Resource Delta
keywords: development, fhir, resource, practitioner
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_practitioner_resource.html
summary: "Practitioner resource delta between GP Connect and the base FHIR resource."
---

Overview of changes made to the standard FHIR&reg; DSTU2 [Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html){:target="_blank"} resource for use within the GP Connect APIs.

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
			<td>	name	</td>
			<td>	0..1	</td>
			<td>	1..1	</td>
			<td>	Practitioner name.	</td>
		</tr>
		<tr>
			<td>	photo	</td>
			<td>	0..*	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	qualification	</td>
			<td>	0..*	</td>
			<td>	0..0	</td>
			<td>	Not defined in current profile, however this may be added and required in a future release.	</td>
		</tr>
	</tbody>
</table>

{% include links.html %}