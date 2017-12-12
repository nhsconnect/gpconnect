---
title: Product versioning
keywords: development, versioning
tags: [development]
sidebar: overview_sidebar
permalink: design_product_versioning.html
summary: An overview of how capability packs (and other technical assets) are versioned.
---

## Product Versioning ##

Versioning of each technical product or asset (for example, API capability pack, design principle(s), data library) is managed using [Semantic Versioning 2.0.0](http://semver.org/){:target="_blank"}.

### Semantic Versioning ###

Given a version number MAJOR.MINOR.PATCH, increment the:

- MAJOR version when you make incompatible API changes
- MINOR version when you add functionality in a backwards-compatible manner, and
- PATCH version when you make backwards-compatible bug fixes

Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

A pre-release version MAY be denoted by appending a hyphen (refer to [Semantic Versioning - Item 9](http://semver.org/#spec-item-9){:target="_blank"})

For example, 1.0.0-alpha.1 is a valid pre-release version.

### Pre-release labels ###

The following pre-release labels will be used across all products:

| Pre-release label | Lifecycle | Description |
|-------------------|-----------|-------------|
| `alpha` | &nbsp; | Complete enough for internal testing. |
| `beta` | early | Complete enough for external testing. |
| `beta` | late | Complete enough for external testing. Usually feature complete. |
| `rc` | &nbsp; | Almost ready for final release. No new feature enhancements. |

> rc = Release Candidate. 

### Maturity Levels ###

{% include todo.html content="The following table is published as a **work in progress** version and as such is subject to change and extension." %}

Taking a similar approach to the [FHIR Maturity Model](http://wiki.hl7.org/index.php?title=FHIR_Maturity_Model){:target="_blank"} GP Connect will only freeze/master a technical specification once it has been independently implemented in at least three commercial systems and demonstrated to interoperate.

| Level | Version | Description | 
|-------|---------|-------------| 
| 1 | `X.Y.Z-alpha.n` | Alpha; rapid iterations, fail fast, exploration, proof of concepts, approach flexible. | Draft may not have been implemented at all but has been published. |
| 2 | `X.Y.Z-beta.n` | Early Beta; rapid iterations, community engaged, scope flexible, high-level approach agreed in principle. | Draft partially implemented in one or more prototype systems. |
| 3 | `X.Y.Z-beta.n` | Late Beta; slower iterations, community engaged, scope largely agreed, high-level approach fixed. | Draft partially implemented two or more commercial systems. |
| 4 | `X.Y.Z-rc.n` | Release candidate; slower iterations, community engaged, scope fixed, detailed approach fixed, no new features, bug fixes and amendments for clinical safety and information governance only. | Draft implemented in at least two commercial systems. |
| 5 | `X.Y.Z` | Stable; release version. | Draft implemented in at least three commercial systems with full accreditation and assurance mechanisms in place. |

