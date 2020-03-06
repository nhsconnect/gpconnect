---
title: Integrate with Spine
keywords: develop
tags: [development]
sidebar: overview_sidebar
toc: false
pathways: [consumer,provider]
permalink: overview_spine_integration.html
summary: Integrate with the NHS Spine
---

To retrieve data from a provider supplier, your application will need to integrate with the Spine as follows:

<p>1. Make a request to the Personal Demographics Service (PDS) to retrieve patient's registered practice.</p>
<p>2. Make a call to the Spine Directory Service (SDS) to retrieve provider endpoint information.</p>
<p>3. Using the endpoint information retrieved in step 2, make a request via Spine Secure Proxy (SSP) to the provider.</p>
<p>4. SSP passes request to provider system.</p>
<p>5. Provider returns data to SSP.</p>
<p>6. SSP passes data to consumer.</p>

![Img](images/integration/gp_connect_apis.png)

For more details on consumer request interactions, see the [SSP implementation guide](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html).

