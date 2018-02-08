---
title: GP Connect Specification Versions
keywords: about
tags: [getting_started]
sidebar: overview_sidebar
toc: false
permalink: overview_specification_versions.html
summary: "Published GP Connect spcification versions"
---

The table below contains the official releases of the GP Connect specification.

{% include important.html content="The current published version are as specified but if you are building Appointments and Foundations you should build against the latest version of the specification. If you are building HTML you should build against the '0.5.0' version of the specification, released on 13th Oct 2017.<br/><br/>The core part of the specification between the DSTU2 and STU3 releases have changed and therefore the versions are not compatible and have been assigned a different major version number." %}

<table>
	<tr>
		<th class="tableColumn15">Release Version</th>
		<th class="tableColumn15">Release Date</th>
		<th class="tableColumn30">Historical Versions</th>
		<th>Details</th>
		<th>Testing</th>
	</tr>
	<tr class="tableSubHeading">
		<th>STU3</th>
		<th/>
		<th/>
		<th/>
		<th/>
	</tr>
	<tr>
		<td><a href="https://developer.nhs.uk/apis/gpconnect-TBC/">1.1.0</a></td>
		<td>TBC</td>
		<td>GP Connect Core rc.2,<br/>
			Foundations rc.5,<br/>
			Appointments rc.4
		</td>
		<td>Appointment slot availability managment and general specification uplift.</td>
		<td><a href="">Automated Test Suite</a></td>
	</tr>
	<tr>
		<td><a href="https://developer.nhs.uk/apis/gpconnect-18Jan2018/">1.0.0</a></td>
		<td>18 Jan 2018</td>
		<td>GP Connect Core rc.1,<br/>
			Foundations rc.4,<br/>
			Appointments rc.3
		</td>
		<td>STU3 Update for Foundations and Appointment. Uplift of the core, cross cutting, areas of the specification.</td>
		<td><a href="">Automated Test Suite</a></td>
	</tr>
	<tr class="tableSubHeading">
		<th>DSTU2</th>
		<th/>
		<th/>
		<th/>
		<th/>
	</tr>
	<tr>
		<td><a href="https://developer.nhs.uk/apis/gpconnect-13Oct2017/">0.5.0</a></td>
		<td>13 Oct 2017</td>
		<td>Access Record HTML rc.5,<br/>
			Appointments rc.2,<br/>
			Foundations rc.3
		</td>
		<td>Access Record HTML rc.5 release.</td>
		<td><a href="https://github.com/nhsconnect/gpconnect-provider-testing/releases/tag/Foundations_RC3_Appointments_RC2">Automated Test Suite</a></td>
	</tr>
</table>

## Historical versioning model ##

Versioning of the GP Connect specificationhas been historically done using a seperate version for each area of the specification, the cross funtional requiremnet have one version and each of the different capability packs, such as Appointment Mangement and Access Record HTML, have their own versions.

The spec has been in a rapid development cycle with lots of change and updates based on analysis of requirements and feedback. Throughout this rapid development cycle the analysis and validating has focused on one capability packs at a time, moving onto the next area of the specification when the previous one has been updated and validated. When we move from FHIR DSTU2 to STU3 the process of working on one area of the spec at a time resulted in a breaking miss match between different areas of the spec, this lead to a re-evaluation of the way GP Connect does specification versioning.


## Current versioning model ##

Rather than versioning the different parts of the spec with different release versions, GP Connect has moved to a model where the whole spec will be versioned under a single version which respresents a snapshot of the spec at that point in time.

## Release version roadmap ##

The following diagram shows the current released versions, the intended releases in the near future and which capability packs are included in each release version:

![Img](images/overview/versionRoadmap.png)