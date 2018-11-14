---
title: Interaction | Delete
keywords: usecase, CareConnect-RARecord-Condition-1
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_interactions_delete.html
summary: Delete describes the interaction required to close or delete an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API. [To remove the whole Reasonable Adjustment Flag, the Remove Flag operation can be used.]
---
{% include custom/search.warnbanner.html %}

Note: the only update allowed to any part of a Reasonable Adjustment record is an update to status (of status = active > inactive).
Any corrections to an already committed Reasonable Adjustment element therefore requires delete of the existing item, then creation of a new Flag, Adjustment or Impairment resource.


## Delete Resource ##

This pattern applies to deletion of a single resource.
* Consent, Flag, Condition and List always use this pattern for deletion.
* Delete Condition triggers Update List if there is an existing List - if there is a Condition to delete, there should _always_ be a List

<img src="images/sequenceDiagrams/UpdateResource.png">

### Delete Resource request - response ###

Given pre-requisites:
- authenticated, authorized RBACed Spine-User
- validated NHSNumber

#### Delete Resource Request ####

For each resource 
```
PUT https://clinicals.spineservices.nhs.uk/STU3/[resourceType]/[id] /HTTP1.1
```

#### Delete Resource Response ####

200 OK http response code (and mirror PUT payload)  
(or operation outcome if failure to find or process)

## Delete Condition resources ##

The Condition resource is pointed to by a List.  
After successful deletion of the Condition resource (see the Delete Resource pattern above), the Client must update the List instance 


<img src="images/sequenceDiagrams/UpdateConditionList.png">

There is no specific http request here.  
The pattern consists of sequenced _Delete Condition_ and _[Update List](/design_interactions_update.html)_ interactions.

Updates to List resources SHALL comply with [Resource Versioning](../../explore/explore_versioning.html) requirements  
and include an If-Match header containing the resource version id ETag (see below).



## Managing Conflicting Updates ##

There is a risk in some cases that two clients will try to update the same resource. If both clients had the same version of that resource to begin with, there is a risk that the second overwrites the updates of the first. To prevent this happening, clients MUST submit update requests with an If-Match header that quotes the ETag from the server (see the [versioning page](explore_versioning.html) for details of version IDs). This specifies the version of the resource that their updates should be applied to, so a second attempt to update the same version with different changes can be detected as a conflict and rejected (this is also known as optimistic locking).

Updates would include the versionID in the HTTP header as follows:

```
PUT https://clinicals.spineservices.nhs.uk/STU3/Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a
If-Match: W/"25777f7d-27bc"
```

If the version Id given in the If-Match header does not match, the server returns a 409 Conflict status code instead of updating the resource.

**IMPORTANT NOTE**: All updates to resources defined in this API MUST include an If-Match header or they will be rejected. The server SHALL return a 412 Precondition Failed in this case.
