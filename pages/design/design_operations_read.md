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

