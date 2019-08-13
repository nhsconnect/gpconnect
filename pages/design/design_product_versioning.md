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
- **Minor** version when larger *non-breaking changes* or *unsubstantive breaking changes* are made, for example a new capability; or a significant number of smaller *non-breaking changes* or *unsubstantive breaking changes* are made
- **Patch** version when smaller *non-breaking changes* or *unsubstantive breaking changes* are made

### Types of change ###

#### Breaking changes ####

*Breaking changes* are those changes made to the specification that require a provider to update their GP Connect API implementation and would cause a consuming system built to any minor or patch version of the same major version of the specification to break.

*Breaking changes* are therefore issued in a new major version of the specification, in order to allow consuming systems built to previous versions to continue to operate at the previous major version without breaking.

#### Unsubstantive breaking changes ####

An *breaking change* may be classified as an *unsubstantive breaking change* where:

- providers and consumers have not built against any minor or patch version of the same major version of the specification, and therefore the change is not breaking in practice

- or in consultation with providers and/or consumers, where providers and/or consumers are in the process of building against any minor or patch version of the same major version of the specification

Where this occurs, previous minor or patch versions of the specifications will either be discontinued ([see below](#pre-release-draft-labels)), or will be amended to include warnings regarding the changed functionality, to ensure consuming (and providing systems) do not build against the changed functionality in the future.

#### Non-breaking changes ####

*Non-breaking changes* are: 

- changes made to the specification that do not require a provider to update their API implementation
- changes made to the specification that do require a provider to update their API implementation but do not cause a consuming system built to any minor or patch version of the same specification to break
- or other types of guidance or supporting material not classified above

#### Stylistic changes and clarifications ####

The version number may not be incremented when *stylistic changes* are made for example, section renumbering, broken links, style corrections, typos, and improvements to the clarity of wording that do not change the meaning of the specification.

### Pre-release (draft) labels ###

When a **pre-release label** is appended to the version number with a hyphen it indicates the specification is still in draft, or has been discontinued.

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
- [Interactive API documentation](system_swagger.html)
- [Provider automated test suite](testing_deliverables.html)
- SDS interaction IDs ([see below](#sds-interaction-ids))
- Service Root URL format ([see below](#service-root-url-format))

The following GP Connect artefacts are released alongside the specification, but use their own version number scheme:

- [FHIR profiles](development_fhir_resource_guidance.html)

### SDS interaction IDs ###

[SDS interaction IDs](development_fhir_operation_guidance.html#foundations-capability-interactions) change only when a new major version of the specification is released and are suffixed with the major version number, except for GP Connect versions 0.x.x where there is no suffix.

### Service Root URL format ###

[Service Root URL formats](development_general_api_guidance.html#service-root-url-versioning) contain the major version number of the specification.
