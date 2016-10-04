---
title: Slot Resource Delta
keywords: development, fhir, resource, slot
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_slot_resource.html
summary: "Slot resource delta between GP Connect and the base FHIR resource."
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
			<td>	An identifier used to identify the slot	</td>
		</tr>		
		<tr>
			<td>	schedule	</td>
			<td>	1..1 Reference(Schedule)	</td>
			<td>	1..1 Reference(Schedule)	</td>
			<td>	The schedule resource that this slot defines an interval of status information -uses 'gpconnectschedule-1' profile	</td>
		</tr>
	</tbody>

</table>


