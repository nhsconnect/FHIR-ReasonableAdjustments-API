---
title: Operation | Determine Provenance
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_operations_provenance.html
summary: Provenance operation describes the server-side operations required to populate, cache and return Provenance information (Practitioner and Organisation information) for all Reasonable Adjustment Flag components on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## Provenance ##

All Reasonable Adjustment resources (Consent, Flag, Condition) are populated server-side with Provenance details on creation to support clinical safety and audit recording. **NB:** List resources do **NOT** record Provenance.

To illustrate, on Create of a resource e.g. a Flag resource (i.e. an Adjustment)
* ClientSystem submits the practitioner's URPId as part of the Create request JWT token
* Spine determines Practitioner, Organization details based on the URPId
* Resource's Provenance is populated with a display representation of the Practitioner, Organization details
* Resource is persisted
* Create response issued to ClientSystem - usually with the created resource as body

[To be clear, on Create, client-side a RARecord Resource will contain no Provenance information.  
Similarly, on Update, Provenance information regarding the updater is produced etc. as part of the Update operation.]

<img src="images/sequenceDiagrams/Provenance.png">

Fine detail of the structure and content of the contained Provenance resource is on the Profile page under [RARecord-Provenance-1](explore_profile.html#RARecord-Provenance-1)
