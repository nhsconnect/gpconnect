---
title: Bundle Resource Delta
keywords: development, fhir, resource, bundle
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_bundle_searchset_resource.html
summary: "Bundle (Searchset) resource delta between GP Connect and the base FHIR resource."
---

Overview of changes made to the standard FHIR&reg; DSTU2 [Bundle](https://www.hl7.org/fhir/DSTU2/bundle.html){:target="_blank"} resource to allow its usage as a Searchset for use within the GP Connect APIs.
								
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
			<td>	total	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	link	</td>
			<td>	0..*	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	entry	</td>
			<td>	0..*	</td>
			<td>	1..*	</td>
			<td>	Must contain at least one entry.	</td>
		</tr>
		<tr>
			<td>	signature	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
	</tbody>
</table>

{% include links.html %}