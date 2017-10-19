---
title: Specification versioning guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_versioning_specification_guidance.html
summary: "Details of the common versioning for the GP Connect specification"
---

The GP Connect specification is broken up into the following sections allowing for separate releases of the different parts of the specification. The section name and section version of the page being viewed is shown above the navigation menu on the left of the page, just below the NHS Digital logo.

The following sections of the specification are currently individually versioned, allowing them to be published as separate releases:

| Specification Section | What is included in the specification section |
| --- | --- |
| [GP Connect](/index.html) | This section of the specification is targeted at the cross cutting requirements and guidance common to all capabilities. |
| [Design Principles](/designprinciples_maturity_model.html) | This section of the specification relates to the overarching principles used by the GP Connect project when creating and implementing any aspect of the GP Connect specification and project. |
| [Access Record HTML](/accessrecord.html) | This section contains requirements and details for development specific to the Access Record HTML capability. |
| [Access Record REST](/accessrecord_rest.html) |This section contains the requirements and details relating to the Access Record REST capability for access to structured data. |
| [Appointment Management](/appointments.html) | This section of the specification relates to the requirements and implementation details specifically relating to the Appointment Management capabilities. |
| [Foundations](/foundations.html) | This section of the specification relates to the requirements and details required for implementing the Foundation capabilities. |
| [Task Management](/tasks.html) | This section of the specification relates to the requirements and details needed to implement the Task Management capability. |

### Versioning Style ###

Each of the sections above will be versioned using [Semantic Versioning 2.0.0](http://semver.org/){:target="_blank"}, using the format "***MAJOR.MINOR.PATCH***".

The separate components of the version will be updated as per below for each update of the specification:

- MAJOR version when you make incompatible API changes.
- MINOR version when you add functionality in a backwards-compatible manner.
- PATCH version when you make backwards-compatible bug fixes.

In addition a pre-release version MAY be denoted by appending a hyphen (refer to [Semantic Versioning - Item 9](http://semver.org/#spec-item-9){:target="_blank"}) along with a pre-release label for the type of release.

### Pre-release Labels ###

The following pre-release labels will be used across all products:

| Pre-release Label | Lifecycle | Description |
|-------------------|-----------|-------------|
| `alpha` | &nbsp; | Complete enough for internal testing. |
| `beta` | early | Complete enough for external testing. |
| `beta` | late | Complete enough for external testing. Usually feature complete. |
| `rc` | &nbsp; | Release Candidate - Almost ready for final release. No new feature enhancements. |

Example: 1.0.0-alpha.1 is an example of a valid pre-release version.


### Specification Versioning Maturity Levels ###

Taking a similar approach to the [FHIR Maturity Model](http://wiki.hl7.org/index.php?title=FHIR_Maturity_Model){:target="_blank"} GP Connect will only freeze / master a technical specification once it has been independently implemented in at least three commercial systems and demonstrated to interoperate.

| Level | Version | Description | 
|-------|---------|-------------| 
| 1 | `X.Y.Z-alpha.n` | Alpha; rapid interactions, fail fast, exploration, proof of concepts, approach flexible. | Draft may not have been implemented at all but has been published. |
| 2 | `X.Y.Z-beta.n` | Early Beta; rapid iterations, community engaged, scope flexible, high-level approach agreed in principle. | Draft partially implemented in one or more prototype systems. |
| 3 | `X.Y.Z-beta.n` | Late Beta; slower iterations, community engaged, scope largely agreed, high-level approach fixed. | Draft partially implemented two or more commercial systems. |
| 4 | `X.Y.Z-rc.n` | Release Candidate; slower iterations, community engaged, scope fixed, detailed approach fixed, no new features, bug fixes and amendments for clinical safety & IG only. | Draft implemented in at least two commercial systems. |
| 5 | `X.Y.Z` | Stable; release version. | Draft implemented in at least three commercial systems with full accreditation and assurance mechanisms in place. |

