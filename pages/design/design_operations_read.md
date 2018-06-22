---
title: Interaction | Read
keywords: usecase, interaction, operation
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_operations_read.html
summary: Read operation describes interaction required to retrieve and view Reasonable Adjustment Flag, Adjustment or Impairment details from Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1. Read Operation ##


<img src="images/sequenceDiagrams/RAFlag-Read-Productionised.png" style="width:700px;">

## 2. Request - Response ##

### Read Requests ###

#### For Consent and Flags ####

```
GET https://[spineservices.nhs.uk]/flagserver/Consent?
  patient=[nhs#]&status=active&category=RAFlag
GET https://[spineservices.nhs.uk]/flagserver/Flag?
  patient=[nhs#]&status=active&category=RAFlag
```
#### For Conditions ####
Get List and include all item references
```
GET https://[spineservices.nhs.uk]/flagserver/List?
  subject=[nhs#]&clinicalStatus=current&code=[RAFlagCode]
  &_include=List:item.clinicalStatus=active
```
[chained List:item.clinicalStatus=active not required if we don't keep deleted items on list - non deleted items makes the list more a current snapshot]

### Read Responses ###

#### consent() ####
  searchset bundle containing 0..1 consent resource 
  (or operation outcome if failure to find or process)

#### flags() ####
searchset of 0..* active RAFlag adjustments for patient

#### conditionListIncludes() ####
searchset bundle containing 0..1 list and 0..* condition resource

## 3. Caching READs ##

When a client does a READ operation to access a specific resource by ID, it may choose to include an ```If-None-Match``` header to specify the version ID of the latest version they have of that resource (see the [versioning page](explore_versioning.html) for details of version IDs) - for example:

```
GET https://[spineservices.nhs.uk]/flagserver/Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a
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
GET https://[spineservices.nhs.uk]/flagserver/Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a
If-Modified-Since: Wed, 21 Oct 2015 07:28:00 GMT
```


