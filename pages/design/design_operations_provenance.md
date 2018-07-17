---
title: Interaction | Determine Provenance
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_interactions_provenance.html
summary: Provenance operation describes the server-side operations required to populate, cache and return Provenance information (Practitioner and Organisation information) for all Reasonable Adjustment Flag components on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Provenance ##

All Reasonable Adjustment resources (Consent, Flag, Condition) are populated with Provenance details on Creation to support clinical safety and audit recording.

To illustrate, on Create of a resource e.g. a Flag resource (i.e. an Adjustment)
* ClientSystem submits the practitioner's URPId as part of the Create request
* Spine looks up the URPId
  * If available, returns cached Practitioner, Organization details
  * Else, retrieves Practitioner, Organization details and caches
* Resource's Provenance is populated with a display representation of the Practitioner, Organization details
* Resource is persisted
* Create response issued to ClientSystem - usually with the created resource as body

[To be clear, on Create, a RARecord Resource will contin no Provenance information.  
The provenance resource is:  
* generated,
* populated,
* contained,
* cross-referenced
* persisted  
server-side as part of the Create operation for the parent resource.  
Similarly, on Update, Provenance information regarding the updater is produced etc. as part of the Update operation.]

  ```
[seq ]
Client                 Spine                    Redis              SDS
   |                     |                        |                |
   | -- Create Rqst ->   |                        |                |
   |    {JWT & URPId}    |                        |                |
   |    (i.e. SDS OrgPersonRoleId)                |                |
   |                     |                        |                |
   |                     |                        |                |
   |                     |                        |                |
   |                     | -- SDS Redis lookup -> |                |
   |                     |                        |                |
--------------------------------------------------------
[Alt]                  |                        |
   |[URPId cached        |                        | -> Get cached
   | in Redis    ]       |                        |    Practitioner,
   |                     |                        | <- Organization details
   |                     |                        |
--------------------------------------------------------
   |                     |                        |                |
   |[URPId not cached]   |                        | -- Get    ---> |
   |                     |                        |    Practitioner,
   |                     |                        | <- Organization details
   |                     |                        |                |
   |                     |                        | -> Cache
   |                     |                        |    Practitioner,
   |                     |                        | <- Organization details
   |                     |                        |
--------------------------------------------------------
   |                     |                        |
   |                     | <- SDS Redis response- |
   |                     |                        |
   |                     | ->Provenance refs      |
   |                     | <-filled Practnr, Org  |
   |                     |                        |
   |                     | ->Persist Flag         |
   |                     | <-with contained       |
   |                     | <-Provenance           |
   |                     |                        |
   |                     | ->Fill display text    |
   |                     | <-for Practnr, Org     |
   |                     |                        |
   | <-Create Response-- |                        |
   |   {Flag}            |                        |
```
Each Reasonable Adjustment resource contains its Provenance information.
Fine detail of the content is on the Profile page under [RARecord-Provenance-1](explore_profile.html#RARecord-Provenance-1)
