---
title: Interaction
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design.html
summary: Interaction describes the interactions and operations that exchange Reasonable Adjustment information via Spine using the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}


## Interactions ##

Interactions are the http request-response exchanges between client and server which are used to fulfil the operations above. These are part of the API.

There isn't a 1 to 1 correspondence to the operations, as for example, 'Add an Impairment' requires 'Create Condition' and either 'Create List' or 'Update List' Interactions, 'Determine Provenance' isn't an http interaction at all.

* _Create Consent_
* _Create Flag_

Both use the _Create Resource_ interaction pattern

* _Create Condition_ 

uses a different interaction incorporating the containing List. 

<br>
* _Read Consent_
* _Read Flag_
* _Read List_

All use the _Read Resource_ pattern  

Update is used to soft delete resources - i.e. once written, the only updateable element is .status active => inactive
<br><br>
* _Update Consent_
* _Update Flag_

Both use the _Update Resource_ pattern

* _Update Condition_ 

uses a different interaction incorporating the containing List.
<br><br>

Interactions are described using Sequence Diagrams in the sections below.  
The Remove Flag and Determine Provenance Operations are also discussed. 
<br>
Interactions and Operations are further illustrated in the _Use Cases & Examples_ section.

<div class="alert alert-warning" role="alert">
<i class="fa fa-warning"></i> <b>Important:</b> For most Developers, the Endpoints page will be a more familiar entry point to understanding the functionality requiredto integrate with the FHIR&reg; Reasonable Adjustments API.<br></div>

## Operations ##

Operations are the set of business activities a user needs to collect, consider and curate Reasonable Adjustments information on behalf of a patient. Users access this functionality through a Reasonable Adjustments client system.  

Operations aren't technically part of the API - they are Client system functional requirements. Here they are used to illustrate/assure that the Interactions (which are part of the API specification) cover the functional scope of the Reasonable Adjustments system.  

Reasonable Adjustments requires the ability to:

* _Add Consent_
* _Add an Adjustment_
* _Add an Impairment or Underlying Condition_
<br>
* _View Consent_
* _View Adjustments_
* _View Impairments, Threshold Code or Underlying Conditions_
<br>
* _Remove an Adjustment_
* _Remove an Impairment or Underlying Condition_
<br>
* _Remove Flag_
* _Determine Provenance_
<br>