---
title: Known issues
keywords: htmlgetcarerecord, getcarerecord, design, known issues, bugs
tags: [htmlgetcarerecord,design]
sidebar: accessrecord_sidebar
permalink: accessrecord_known_issues.html
summary: "Known issues related to the Access Record capability"
---
<a href="#" class="back-to-top">Back to Top</a>

## Specification documentation ##

This list is of known issues at the time of publication of this version of the specification. Issues which are identified after publication will be record as tickets on github which can be viewed [here](https://github.com/nhsconnect/gpconnect/issues) 

- The section content is not fully specified in some of the HTML sections to enable the providers to provide content which best represents the nature of the information captured in their system. This issue recognises the differences across providers. Providers should use the section and subsection content banner to state limitations, business logic for the content, or known variances.

- Some section and subsection content banner messages have been included to assist providers and consumers to understand content population across the providers, for instance to assist consumers to scope test and training activities. These are examples only. Individual provider content messages are not mandated by the specification and may be changed by providers without update to the applicable specification version.

- The specification references external resources in places. The links may be impacted by changes and may require maintenance over time.

- Any limitation to compliance with accessibility standards caused directly by the specification for Access Records HTML are accepted.

 

## Known issues with provider variance ##

- XML is not supported by all providers.

- Some sections/subsections are not supported by some providers. Check each section description in the HTML views for details. 

- The scope of the contents for sections and subsections will sometimes vary across providers. Where variances are known, these are described in the sample provider content banner details in each of the HTML view section descriptions.  

- Not all provider variances (differences between the content returned by each provider within the scope of the specification) are listed within this specification. Consumers should consider this in their testing and training approaches.
