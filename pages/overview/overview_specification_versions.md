---
title: Specification versions
keywords: about
tags: [getting_started]
sidebar: overview_sidebar
toc: false
permalink: overview_specification_versions.html
summary: "Directory of published GP Connect specification versions"
---

{% include custom/versionconfig.html %}

{% if showVersionsPage != "true" %}

Please refer the [latest Versions page](https://nhsconnect.github.io/gpconnect/overview_specification_versions.html).

{% else %}

### Introduction ###

GP Connect specification releases are assigned a single version number from 23 February 2018 onwards. The automated test suite, demonstrator and other artefacts built against the specification will also be assigned the same single version number.

This single version number scheme supercedes the previous scheme whereby the constituent capability packs were released and versioned seperately (Access Record HTML, Appointments etc).

Versions 0.x.x are based on the FHIR&reg; DSTU2 standard and versions 1.x.x are based on the FHIR&reg; STU3 standard.


### Released specification versions ###

The table below contains the official released versions of the GP Connect specification:

{% include important.html content="The Access Record HTML capability is currently only available in 0.x.x (DSTU2) versions of the specification. Appointments Management and Foundations capabilities are available in the 1.x.x (STU3) versions of the specification, where further capabilites will also be added as announced." %}

<table>
	<tr>
		<th class="tableColumn15">Release Version</th>
		<th class="tableColumn15">Release Date</th>
		<th class="tableColumn15">Containing capabilities</th>
		<th>Details</th>
	</tr>
	<tr class="tableSubHeading">
		<th colspan="4">GP Connect 1.x.x (STU3) versions</th>
	</tr>
	<tr>
		<td><a href="https://developer.nhs.uk/apis/gpconnect-18Jan2018/">GP Connect 1.0.0</a><p><i>(current 1.x.x)</i></p></td>
		<td>23 Feb 2018</td>
		<td>Appointments, Foundations</td>
		<td>STU3 update for Foundations and Appointments. Uplift of the core and cross cutting areas of the specification.<p>Previously released on 18 Jan 2018 as GP Connect Core rc.1, Foundations rc.4, Appointments rc.3 under the old version scheme.</p>
		<p>Artefacts at this version: <a href="https://developer.nhs.uk/apis/gpconnect-18Jan2018/">Specification</a>, <a href="https://github.com/nhsconnect/gpconnect-provider-testing/releases/tag/GP_Connect_Core_RC1_Foundations_RC4_Appointments_RC3">Automated test suite</a>, <a href="http://ec2-54-194-109-184.eu-west-1.compute.amazonaws.com/">Demonstrator</a></p>
		</td>
	</tr>
	<tr class="tableSubHeading">
		<th colspan="4">GP Connect 0.x.x (DSTU2) versions</th>
	</tr>
	<tr>
		<td><a href="https://developer.nhs.uk/apis/gpconnect-13Oct2017/">GP Connect 0.5.0</a><p><i>(current 0.x.x)</i></p></td>
		<td>23 Feb 2018</td>
		<td>Access Record HTML</td>
		<td>Access Record HTML rc.5 release.<p>Previously released on 13 Oct 2017 as Access Record HTML rc.5 under the old version scheme.</p>
		<p>Artefacts at this version: <a href="https://developer.nhs.uk/apis/gpconnect-13Oct2017/">Specification</a>, <a href="https://github.com/nhsconnect/gpconnect-provider-testing/releases/tag/AppointmentsRc.2%2CFoundationsRc.3">Automated test suite</a>, <a href="http://ec2-54-194-109-184.eu-west-1.compute.amazonaws.com:380/">Demonstrator</a></p>
		</td>
	</tr>
</table>

### Pre-release (draft) specification versions ###

The specification versions in this table are currently issued as pre-release (draft) versions of the specification and are subject to change:

{% include warning.html content="Pre-release (draft) specifications are subject to change and intended for review purposes only. Do not build against these specifications unless agreed with NHS Digital. " %}

<table>
	<tr>
		<th class="tableColumn15">Pre-release Version</th>
		<th class="tableColumn15">Pre-release Date</th>
		<th class="tableColumn15">Containing capabilities</th>
		<th>Details</th>
	</tr>
	<tr class="tableSubHeading">
		<th colspan="4">GP Connect 1.x.x (STU3) versions</th>
	</tr>
	<tr>
		<td><a href="https://developer.nhs.uk/apis/gpconnect-TBC/">GP Connect 1.1.0-rc</a><p><i>(pre-release)</i></p></td>
		<td>25 Feb 2018</td>
		<td>Appointments, Foundations</td>
		<td>Appointment slot availability managment and general specification uplift.<p>Previously named as GP Connect Core rc.2, Foundations rc.5, Appointments rc.4 under the old version scheme, though not released under this scheme.</p>
		<p>Artefacts at this version: <a href="https://developer.nhs.uk/apis/gpconnect-TBC/">Specification</a></p>
		</td>
	</tr>
	<tr class="tableSubHeading">
		<th colspan="4">GP Connect 0.x.x (DSTU2) versions</th>
	</tr>
	<tr>
		<td colspan="4"><i>(no current pre-release versions are available)</i></td>
	</tr>
</table>

{% endif %}
