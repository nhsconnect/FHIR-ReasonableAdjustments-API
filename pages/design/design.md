---
title: Interaction
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecordrestsidebar
permalink: design.html
summary: Interaction describes the interactions and operations that exchange Reasonable Adjustment information via Spine using the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## Operations ##

Operations are the set of business activities a user needs to collect, consider and curate Reasonable Adjustments information on behalf of a patient. Users access this functionality through a Reasonable Adjustments client system.  

Operations aren't part of the API - they are Client system functional requirements. Here they are used to illustrate/assure that the Interactions (which are part of the API) cover the functional scope of the Reasonable Adjustments system.  

Reasonable Adjustments requires the ability to:
<br>
* Add Consent
* Add an Adjustment
* Add an Impairment  
<br>
* View Consent
* View Adjustments
* View Conditions  
<br>
* Remove Consent
* Remove an Adjustment
* Remove an Impairment  
<br>
* Remove Flag
* Determine Provenance  


## Interactions ##

Interactions are the http request-response exchanges between client and server which are used to fulfil the operations above. These are part of the API.

There isn't a 1 to 1 correspondence to the operations, as for example, 'Add an Impairment' requires 'Create Condition' and either 'Create List' or 'Update List' Interactions, 'Determine Provenance' isn't an http interaction at all.
<br>
* Create Consent
* Create Flag

Both use the Create Resource interaction pattern
<br>
* Create Condition 

uses a different interaction incorporating the containing List. 
<br>
* Read Consent
* Read Flag
* Read List

All use the Read Resource pattern  

<br>
Update is used to soft delete resources - i.e. once written, the only updateable element is .status active => inactive
<br>
* Update Consent
* Update Flag

Both use the Update Resource pattern

* Update Condition 

uses a different interaction incorporating the containing List.
<br>

Interactions are described using Sequence Diagrams in the sections below.  
The Remove Flag and Determine Provenance Operations are also discussed. 
<br>
Interactions and Operations are further illustrated in the Use Cases & Examples section.
