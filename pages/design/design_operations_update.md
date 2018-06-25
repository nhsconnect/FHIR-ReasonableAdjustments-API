---
title: Interaction | Update
keywords: usecase, CareConnect-RARecord-Condition-1
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_operations_update.html
summary: Update operation describes interaction required to update a new Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1. Update Operation ##

Note: the only update allowed to any part of a Reasonable Adjustment record is an update to status (essentially a soft delete, as status = active > inactive).
Any corrections to an already committed Reasonable Adjustment element therefore requires update of the existing item, then creation of a new Flag, Adjustment or Impairment resource.


<img src="images/sequenceDiagrams/RAFlag-Update-Productionised.png" style="width:700px;">

## 2. Request - Response ##

### Update Consent or Flag resource ###

#### Update Requests ####

For each updated resource of type Consent or Flag (only 'status = active' > 'status = inactive' allowed)
##### update Resource() #####
```
PUT [spineservices.nhs.uk]/flagserver/[resource]/[id]
```
#### Update Responses ####

##### updatedResource() #####

  200 http response code (and mirror PUT payload)
(or operation outcome if failure to find or process)

### Update List and Condition resources ###

#### Update Requests ####

- Each updated/closed 'Disability Type' line item bundled as Condition in Transaction bundle
- List is updated with relevant entry element set to List .entry.deleted=true

##### sendTransaction() #####
```
  POST https://[spineservives.nhs.uk]/flagserver
```
Transaction bundle demarshalled at POST endpoint and each Bundle.entry.request then performed separately, as per FHIR specification below

Within the Transaction i.e. at Bundle.entry.request, http requests are:

###### update Condition() ######
```
PUT https://[spineservices.nhs.uk]/flagserver/Condition/[Id]
```
###### update List() ######
```
PUT https://[spineservices.nhs.uk]/flagserver/List /[Id]
```



#### Update Responses ####

#### successResponse() ####

  200 http response code and transaction-response bundle 
(or operation outcome if failure to find or process)

#### failResponse() ####

  4xx or 5xx http response code and operation outcome describing failure

## 3. Managing Conflicting Updates

There is a risk in some cases that two clients will try to update the same resource. If both clients had the same version of that resource to begin with, there is a risk that the second overwrites the updates of the first. To prevent this happening, clients MUST submit update requests with an If-Match header that quotes the ETag from the server (see the [versioning page](explore_versioning.html) for details of version IDs). This specifies the version of the resource that their updates should be applied to, so a second attempt to update the same version with different changes can be detected as a conflict and rejected (this is also known as optimistic locking).

Updates would include the versionID in the HTTP header as follows:

```
PUT /Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a
If-Match: W/"25777f7d-27bc"
```

If the version Id given in the If-Match header does not match, the server returns a 409 Conflict status code instead of updating the resource.

**IMPORTANT NOTE**: All updates to resources defined in this API MUST include an If-Match header or they will be rejected.
