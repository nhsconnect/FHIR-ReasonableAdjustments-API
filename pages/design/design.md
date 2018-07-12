---
title: Interaction
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design.html
summary: Interaction describes ReSTful interactions and operations required to exchange Reasonable Adjustment information via Spine using the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Operations ##

Operations are the set of activities (i.e. functional requirements) needed to exchange Reasonable Adjustment information across the FHIR-ReasonableAdjustments-API (so it can be nationally stored and available).  

These aren't technically part of the API. Strictly, they are Client system functional requirements, describing functionality required by the end-user. Here they are used to illustrate/assure that the Interactions (which are part of the API) cover the functional scope of the Reasonable Adjustments system.  

Reasonable Adjustments requires the ability to:

* _Add Consent_
* _Add an Adjustment_
* _Add an Impairment_  
<br>
* _View Consent_
* _View Adjustments_
* _View Conditions_  
<br>
* _Remove Consent_
* _Remove an Adjustment_
* _Remove an Impairment_  
<br>
* _Remove Flag_
* _Determine Provenance_  
    (Need to demonstrate how the solution design produces the Provenance resource/information in the created/persisted resource. Basically, we feed it the URPId as part of the http request, server uses this to generate a Provenance resource, this is contained in the parent/container resource and persisted.)

## 2 Interactions ##

Interactions are the http request response exchanges between client and server which fulfil the operations above.  

There isn't a 1 to 1 correspondence to the operations, as for example, 'Add an Impairment' requires 'Create Condition' and either 'Create List' or 'Update List' Interactions, and 'Determine Provenance' isn't an http interaction at all.


To do:
    rewrite pages with better UCs


Create Consent
    Create Consent request
        POST https://clinicals.spineservices.nhs.uk/STU3/Consent HTTP/1.1
        Example OK
    Create Consent response

Create Flag
    Create Flag request

    Create Flag response

Create Condition
    Create Condition request
    Create Condition response

Create List
    Create List request
    Create List response

Read Consent
    Read Consent request
    Read Consent response

Read Adjustments
    Read Adjustments request
    Read Adjustments response

Read Conditions
    Read Conditions request
    Read Conditions response

Read List
    Read List request
    Read List response

Update List
    Update List request
    Update List response

Delete Consent
    Delete Consent request
    Delete Consent response

Delete Flag
    Delete Flag request
    Delete Flag response

Delete Condition
    Delete Condition request
    Delete Condition response

Delete List
    Delete List request
    Delete List response