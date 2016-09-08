---
title: Schedule Resource Delta
keywords: development, fhir, resource, schedule
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_schedule_resource.html
summary: "Schedule resource delta between GP Connect and the base FHIR resource."
---
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
			<td>	An identifier used to identify the schedule	</td>
		</tr>		
		<tr>
			<td>	type	</td>
			<td>	0..*	</td>
			<td>	0..1	</td>
			<td>	Type of appointment schedule	</td>
		</tr>
		<tr>
			<td>	actor	</td>
			<td>	1..1	</td>
			<td>	1..1	</td>
			<td>	The resource this Schedule resource is providing availability information for - uses 'gpconnect-location-1' profile	</td>
		</tr>
	</tbody>

</table>

{% include links.html %}