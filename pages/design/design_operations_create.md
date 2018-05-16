---
title: Interaction | Create
keywords: usecase, CareConnect-RARecord-Condition-1
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_operations_create.html
summary: Create operation describes interaction required to record a new Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1. Create Operation ##

<img src="images/sequenceDiagrams/RAFlag-Create-Productionised.png" style="width:700px;">

## 2. Request - Response ##

### Create Consent or Flag resource ###

Given pre-requisites:
- authenticated, authorized RBACed Spine-User
  - SMSP: asid, partykey
  - DIP: IDToken, AccessToken
- validated NHSNumber

#### Create Requests ####

For each new resource i.e. new Consent|Flag
```
POST https://[spineservices.nhs.uk]/flagserver/[resource]
```

#### Create Response ####

201 http response code and Location header (and mirror POSTed payload)
(or operation outcome if failure to find or process)

### Create List and Condition resources ###

#### Create Requests ####

For each new 'Disability Type' line item bundled as Condition in Transaction bundle, 
List is created or updated with new entry element, with temporary intra-bundle referencing to temp Condition.id

##### sendTransaction() #####
```
  POST https://[spineservives.nhs.uk]/flagserver
```
Transaction bundle is demarshalled at the POST endpoint and each Bundle.entry.request is then performed separately, as per [FHIR specification](http://hl7.org/fhir/http.html#transaction)

Within the Transaction i.e. values at Bundle.entry.request, http requests are:

##### create Condition() #####
```
POST https://[spineservices.nhs.uk]/flagserver/Condition
```
##### create List() #####
```
POST https://[spineservices.nhs.uk]/flagserver/List
```

#####  update List() #####
```
PUT https://[spineservices.nhs.uk]/flagserver/List /[ListId]
```


#### Create Response ####

##### successResponse() #####

  200 http response code and transaction-response bundle 
(or operation outcome if failure to find or process any of the transaction bundle requests)

failResponse()

  40x or 50x http response code and operation outcome describing failure


