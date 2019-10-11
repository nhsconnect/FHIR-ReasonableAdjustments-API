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
* Condition resource - which entails maintaining its containing List


## Create Resource ##

This pattern applies to creation of a single resource.
* Consent and Flag use this pattern for creation.

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

```
201 Created http response code and Location header (and mirror POSTed payload)  
(or operation outcome if failure to find or process)
```

## Create Consent resources ##

Business Rule: Spine Clinicals SHALL NOT allow more than 1 Consent resource to be active for a given NHS Number.

Error response: Spine Clinicals SHALL respond with response code 422 DUPLICATE_REJECTED and an OperationOutcome resource on creation of a duplicate, active Consent resource for an NHS Number.

## Create Condition resources ##

The new Condition resource to be added to the Reaonable Adjustment record is contained in a List.
After successful client-side construction of the new Condition and Provenance resources, the Client must either:
* create a new List instance
* update the existing List instance


<img src="images/sequenceDiagrams/CreateListCondition.png">

### Create Condition request - response ###

Given pre-requisites:
- authenticated, authorized RBACed Spine-User
- validated NHSNumber

#### Create Condition Request (New List)####

```
POST https://clinicals.spineservices.nhs.uk/STU3/List /HTTP1.1
```

#### Create Condition Response (New List)####

```
201 Created http response code and Location header (and mirror POSTed payload)  
(or operation outcome if failure to find or process)
```

#### Create Condition Request (Existing List)####

```
POST https://clinicals.spineservices.nhs.uk/STU3/List /HTTP1.1
```

#### Create Condition Response (Existing List)####

```
200 OK http response code and Location header (and mirror POSTed payload)  
(or operation outcome if failure to find or process)
```
