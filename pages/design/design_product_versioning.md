---
title: Specification versioning
keywords: development, versioning
tags: [development]
sidebar: overview_sidebar
permalink: design_product_versioning.html
summary: An overview of how the specification (and other technical assets) are versioned
---

{% include important.html content="This page describes the standard by which the specification and other artefacts are versioned.  To see a list of specification versions and the capabilities available at those versions, please see the [specification versions](https://developer.nhs.uk/gp-connect-specification-versions/) page." %}

## Introduction ##

**GP Connect specification releases are assigned a single version number from 23 February 2018 onwards.**

The automated test suite, demonstrator and other artefacts released in line with the specification are also assigned the same single version number.

This supersedes the previous scheme whereby the constituent capability packs (Access Record HTML, Appointments etc) were released and versioned independently.

## Version number standard ##

The specification version number is based on the [Semantic Versioning 2.0.0](http://semver.org/){:target="_blank"} standard.

![Semantic versioning diagram](images/design/semantic-versioning.png)

When a specification is released, the version number is incremented as follows:

- **Major** version when *breaking changes* are made
- **Minor** version when larger *non-breaking* changes are made, for example a new capability, or signficant number of small *non-breaking* changes are made
- **Patch** version when smaller *non-breaking* changes are made

*Breaking changes* are those that would break a consuming system built to the previous version of the specification, when communicating with a provider system built to the the new version.

The version number is NOT incremented when *stylistic changes* are made for example, section renumbering, broken links, style corrections, typos, and improvements to the clarity of wording that do not change the meaning of the specification.

### Pre-release (draft) labels ###

When a **pre-release label** is appended to the version number with a hypen it indicates the specifaction is still in draft, or has been discontinued.

{% include important.html content="The pre-release label is used to indicate that a specification is in draft (or has been discontinued), it **does not** indicate that a providing system has made a pre-release of their GP Connect software." %}

The pre-release labels used are as follows:

| Pre-release Label | Example            | Description |
|-------------------|--------------------|-------------|
| `alpha`           | 1.1.0-alpha        | The version of the specification is being authored and is subject to frequent and or major changes. |
| `beta`            | 1.1.0-beta         | The version of the specification is being internally reviewed and is subject to change. |
| `rc`              | 1.1.0-rc           | The version of the specification is being reviewed by external parties including providers and consumers and is subject to corrections and minor change. |
| *(no label)*      | 1.1.0              | The version of the specification is now fixed (immutable).  Further changes (excluding *stylistic change*) require a new version number. |
| `discontinued`    | 1.1.0-discontinued | The version of the specification is no longer relevant and has been discontinued. |

## Associated technical artefacts ##

The following GP Connect artefacts are released as part of or alongside the specification, taking the same version number as the specification:

- [System demonstrator](system_demonstrator.html)
- [Provider automated test suite](testing_deliverables.html)
- SDS interaction IDs (see below)
- Service Root URL format (see below)

### SDS interaction IDs ###

[SDS interaction IDs](development_fhir_operation_guidance.html#foundations-capability-interactions) change only when a new major version of the specification is released and are are suffixed with the major version number, except for GP Connect versions 0.x.x where there is no suffix.

### Service Root URL format ###

[Service Root URL formats](development_general_api_guidance.html#service-root-url-versioning) contain the major version number of the specification.
