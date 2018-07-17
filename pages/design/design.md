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

Operations are the set of business activities a user needs to collect, consider and curate Reasonable Adjustments information on behalf of a patient. Users access this functionality through a Reasonable Adjustments client system.  

These aren't technically part of the API. Strictly, they are Client system functional requirements. Here they are used to illustrate/assure that the Interactions (which are part of the API) cover the functional scope of the Reasonable Adjustments system.  

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
<br>

## 2 Interactions ##

Interactions are the http request-response exchanges between client and server which are used to fulfil the operations above.  

There isn't a 1 to 1 correspondence to the operations, as for example, 'Add an Impairment' requires 'Create Condition' and either 'Create List' or 'Update List' Interactions, 'Determine Provenance' isn't an http interaction at all.

* _Create Consent_
* _Create Flag_
* _Create Condition_
* _Create List_  
<br>
All use the _Create Resource_ pattern  
Condition and List must also consider the _Create Condition_ resources pattern
<br><br>
* _Read Consent_
* _Read Adjustments_
* _Read Conditions_
* _Read List_  
<br>
Consent and Adjustments use the _Read Resource_ pattern  
List and then Condition use _Read List_ followed by _Read Conditions_ pattern
<br><br>
* _Update List_  
<br>
_Update List_ is used when Creating or Deleting Conditions from an existing List
<br><br>
* _Delete Consent_
* _Delete Flag_
* _Delete Condition_
* _Delete List_  
<br>
All use the _Delete Resource_ pattern  
Condition and List must also consider the _Delete Condition_ resources pattern
<br><br>
Interactions are described using Sequence Diagrams in the sections below.  
The Remove Flag and Determine Provenance Operations are also discussed.  
<br>
Interactions and Operations are further illustrated in the _Use Cases & Examples_ section.
