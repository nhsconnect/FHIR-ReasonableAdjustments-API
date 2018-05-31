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

  40x or 50x http response code and operation outcome describing failure



