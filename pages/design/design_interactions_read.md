---
title: Interaction | Read
keywords: usecase, interaction, operation
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_interactions_read.html
summary: Read operation describes interaction required to retrieve and view Reasonable Adjustment Flag, Adjustment or Impairment details from Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

There are 2 common patterns when working with the various Reasonable Adjustment resources within the Interactions:
* Consent and Flag resource - single, independent resources
* Condition resource - which are referenced using their associated List

When reading resources
* Consent and Flag use the _Read Resource_ pattern
* Condition resources use _Read Conditions_

## Read Resource ##


<img src="images/sequenceDiagrams/ReadResource.png">

### Read Resource request - response ###

Given pre-requisites:
- authenticated, authorized RBACed Spine-User
- validated NHSNumber

#### Read Resource Request ####

For each resource type
```
GET https://clinicals.spineservices.nhs.uk/STU3/[resourceType]?
  patient=[nhs#]&status=active&category=RAFlag /HTTP1.1
```

#### Read Resource Responses ####

##### Consent resources #####
  searchset bundle containing 0..1 consent resource  
  (or operation outcome if failure to find or process)  

##### Flag resources #####
  searchset of 0..* active RAFlag adjustments for patient  
  (or operation outcome if failure to find or process)

## Read Conditions ##
The _Read Conditions_ interaction is a sequenced pair of interactions to read the Patient's Reasonable Adjustments List, then to Read only those active Conditions it lists.

<img src="images/sequenceDiagrams/ReadConditionList.png">

### Read Conditions request - response ###

Given pre-requisites:
- authenticated, authorized RBACed Spine-User
- validated NHSNumber

#### Read Conditions Request ####

First reading the List:
```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
  patient=[nhs#]&status=active&category=RAFlag /HTTP1.1
```
On successful read of the List, read the Conditions:
```
GET https://clinicals.spineservices.nhs.uk/STU3/Condition?
  _list=[ListId]&clinical-status=active /HTTP1.1
```
Implementations of _Read Conditions_ MUST implement the Search Parameters \_list and clinical-status for the Condition resource.

#### Read Conditions Responses ####

##### List resource #####
  searchset bundle containing 0..1 list resource  
  (or operation outcome if failure to find or process)  

##### Condition resources #####
  searchset of 0..* active Conditions for patient  
  (or operation outcome if failure to find or process)


##  Caching Reads ##

When a client does a Read operation to access a specific resource by ID, it may choose to include an ```If-None-Match``` header to specify the version ID of the latest version they have of that resource (see the [versioning page](explore_versioning.html) for details of version IDs) - for example:

```
GET https://clinicals.spineservices.nhs.uk/STU3/Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a
If-None-Match: W/"25777f7d-27bc"
```

If the version ID specified in the HTTP header matches the latest held on Spine, a HTTP 304 Not Modified status code will be returned to inform the client that they already have the latest version:

```
HTTP/1.1 304 Not Modified
Date: Mon, 18 Sep 2015 22:20:01 GMT
```

If a newer version of the resource does exist, it will be returned as normal, with the newer versionID as described above so the client can update its cache.

Similarly, a client can query for updates that have a Last-Modified data newer than the last time they queried, by specifying a date in an [If-Modified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since) HTTP header:

```
GET https://clinicals.spineservices.nhs.uk/STU3/Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a
If-Modified-Since: Wed, 21 Oct 2015 07:28:00 GMT
```


