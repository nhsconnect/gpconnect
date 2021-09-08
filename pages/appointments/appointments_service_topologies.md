---
title: Common service topologies
keywords: appointments design
tags: [design,appointments]
sidebar: appointments_sidebar
permalink: appointments_service_topologies.html
summary: "Provider organisation service topologies"
---

<br/>

The topologies on this page show examples of GP practices and other types of GP service, and the configuration required to support booking from Directory of Services (DOS).

### GP practices ###

GP practices running "in hours" GP services for their registered patients only *SHOULD NOT* normally [set up services in their service filtering configuration](appointments_serviceid_configuration.html#service-list) or switch on service filtering in order to accept bookings via Directory of Services (DOS).

{% include important.html content="Despite branch surgeries being listed as separate services on DOS, it is currently (as of Sep 2021) not recommended to enable service filtering in practices that do not run additional types of service such as extended access hubs, due to a restriction in the DOS search algorithm that prevents more than one service of type *GP practice* being returned. This guidance will be reviewed and updated in line with changes to the DOS search algorithm." %}

<img src="images/appointments/service-topologies-1.png" style="padding-bottom: 10px;" />

### GP practices also running extended access hubs ###

GP practices that also run extended access hubs *MAY* configure services within their GP system to mirror the 

<img src="images/appointments/service-topologies-2.png" style="padding-bottom: 10px;" />

### "Standalone" extended access hubs ###

<img src="images/appointments/service-topologies-3a.png" style="padding-bottom: 10px;" />

<img src="images/appointments/service-topologies-3b.png" style="padding-bottom: 10px;" />

