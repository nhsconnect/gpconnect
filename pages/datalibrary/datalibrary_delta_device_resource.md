---
title: Device Resource Delta
keywords: development, fhir, resource, device
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_device_resource.html
summary: "Device resource delta between GP Connect and the base FHIR resource."
---

Overview of changes made to the standard FHIR&reg; DSTU2 [Device](https://www.hl7.org/fhir/DSTU2/device.html){:target="_blank"} resource to allow its usage within the GP Connect APIs.

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
			<td>	0..1	</td>
			<td>	A unique identifier for the device.	</td>
		</tr>
		<tr>
			<td>	type	</td>
			<td>	1..1<br>(GMDC)	</td>
			<td>	1..1<br>(SNOMED)	</td>
			<td>	Type of device - fixed to SNOMED CT Code 462240000 'Patient health record information system (physical object)'</td>
		</tr>
		<tr>
			<td>	note	</td>
			<td>	0..*	</td>
			<td>	0..1	</td>
			<td>	Device notes and comments.	</td>
		</tr>
		<tr>
			<td>	status	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	manufacturerDate	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	expiry	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	udi	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	lotNumber	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	patient	</td>
			<td>	0..1<br>Reference(Patient)	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	contact	</td>
			<td>	0..*	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	url	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
	</tbody>
</table>

{% include links.html %}