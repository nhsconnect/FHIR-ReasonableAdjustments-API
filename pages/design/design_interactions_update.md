---
title: Interaction | Update
keywords: usecase, CareConnect-RARecord-Condition-1
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_interactions_update.html
summary: Update interaction describes the interaction required to update List resources via the FHIR&reg; Reasonable Adjustments API. These are used to manage the Impairments recorded on a Reasonable Adjustment Flag.
---
{% include custom/search.warnbanner.html %}

Note: the only update allowed to any part of a Reasonable Adjustment record is an update to status (essentially a soft delete, as status = active > inactive).  
Any corrections to an already committed Reasonable Adjustment element therefore require removal of the existing item, then creation of a new Flag, Adjustment or Impairment resource.  
<br>
This section describes the _Update List_ interaction used when Creating or Deleting Conditions on an existing List

## 1. Update List ##

The _Update List_ interaction is required in 2 circumstances:
* when a new Impairment (Condition resource) is added to a Reasonable Adjustments record (after the first Impairment)
* when an individual Impairment is deleted from a Reasonable Adjustments record
Once the Condition resource has been created or deleted, the List SHALL be updated accordingly

### After Create Condition ###
<img src="images/sequenceDiagrams/UpdateListNew.png">

### After Delete Condition ###
<img src="images/sequenceDiagrams/UpdateListDelete.png">

### Update List request - response ###

#### Update List Request ####

```
PUT https://clinicals.spineservices.nhs.uk/STU3/List?[List.id] /HTTP1.1
```

#### Update List Response ####

200 OK http response code and (and mirror PUT payload)  
(or operation outcome if failure to find or process)  
<br>
Updates to List resources SHALL comply with [Resource Versioning](/explore_versioning.html) requirements  
and include an If-Match header containing the resource version id ETag (see below).



## 2. Managing Conflicting Updates ##

There is a risk in some cases that two clients will try to update the same resource. If both clients had the same version of that resource to begin with, there is a risk that the second overwrites the updates of the first. To prevent this happening, clients MUST submit update requests with an If-Match header that quotes the ETag from the server (see the [versioning page](explore_versioning.html) for details of version IDs). This specifies the version of the resource that their updates should be applied to, so a second attempt to update the same version with different changes can be detected as a conflict and rejected (this is also known as optimistic locking).

Updates would include the versionID in the HTTP header as follows:

```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/744eec7d-8951-4722-ad74-dc34e86d4e1a
If-Match: W/"25777f7d-27bc"
```

If the version Id given in the If-Match header does not match, the server returns a 409 Conflict status code instead of updating the resource.

**IMPORTANT NOTE**: All updates to resources defined in this API MUST include an If-Match header or they will be rejected. The server SHALL return a 412 Precondition Failed in this case.
