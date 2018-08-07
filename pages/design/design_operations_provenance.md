---
title: Operation | Determine Provenance
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_operations_provenance.html
summary: Provenance operation describes the server-side operations required to populate, cache and return Provenance information (Practitioner and Organisation information) for all Reasonable Adjustment Flag components on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Provenance ##

All Reasonable Adjustment resources (Consent, Flag, Condition) are populated with Provenance details on Creation to support clinical safety and audit recording. **NB:** List resources do **NOT** record Provenance.

To illustrate, on Create of a resource e.g. a Flag resource (i.e. an Adjustment)
* ClientSystem submits the practitioner's URPId as part of the Create request
* Spine looks up the URPId
  * If available, returns cached Practitioner, Organization details
  * Else, retrieves Practitioner, Organization details and caches
* Resource's Provenance is populated with a display representation of the Practitioner, Organization details
* Resource is persisted
* Create response issued to ClientSystem - usually with the created resource as body

[To be clear, on Create, a RARecord Resource will contain no Provenance information.  
The provenance resource is:  
* generated,
* populated,
* contained,
* cross-referenced
* persisted  
server-side as part of the Create operation for the parent resource.  
Similarly, on Update, Provenance information regarding the updater is produced etc. as part of the Update operation.]

<img src="images/sequenceDiagrams/Provenance.png">

Fine detail of the structure and content of the contained Provenance resource is on the Profile page under [RARecord-Provenance-1](explore_profile.html#RARecord-Provenance-1)
