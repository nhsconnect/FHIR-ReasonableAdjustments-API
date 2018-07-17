---
title: Interaction | Create
keywords: usecase, CareConnect-RARecord-Condition-1
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_interactions_create.html
summary: Create operation describes interaction required to record a new Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

There are 2 common patterns when working with the various Reasonable Adjustment resources within the Interactions:
* Consent and Flag resource - single, independent resources
* Condition resource - which entails maintaining its associated List


## 1 Create Resource ##

This pattern applies to creation of a single resource.
* Consent, Flag, Condition and List always use this pattern for creation.
* Create Condition triggers Create List if there is no existing List
* Create Condition triggers Update List if there is an existing List

<img src="images/sequenceDiagrams/CreateResource.png">

### Create Resource request - response ###

Given pre-requisites:
- authenticated, authorized RBACed Spine-User
- validated NHSNumber

#### Create Resource Request ####

For each new resource 
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resourceType] /HTTP1.1
```

#### Create Resource Response ####

201 Created http response code and Location header (and mirror POSTed payload)  
(or operation outcome if failure to find or process)

## 2 Create Condition resources ##

The Condition resource is pointed to by a List.  
After successful creation of the Condition resource (see the Create Consent and Flag pattern above), the Client must either:
* create a new List instance
* update the existing List instance


<img src="images/sequenceDiagrams/CreateConditionList.png">

There is no specific http request here.  
The pattern consists of sequenced _Create Condition_ and _Create List_ or _Update List_ interactions.


