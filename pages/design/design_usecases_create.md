---
title: Interaction | Create
keywords: usecase
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_create.html
summary: Create operation describes interaction required to record a new Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Create RARecord Use Case ##
### Trigger: ###
GP initiates Reasonable Adjustment Flag discussion at annual health check
### Pre-requisites: ###
Practioner Dr D. logged on w SmartCard/National Identity giving URPId (as SDS OrgPersonRole Identifier)  
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB, demographic data  
ClientSystem searched and failed to find existing RARecord  
### System Scope: ###
ClientSystem includes GPSystem client, SCRa, 1-click etc.  
ServerSystem includes Spine, PDS, SDS, FlagServer etc.  
### Summary: ###
Practitioner creates RARecord, recording Consent from Patient and that Impairment is 'Learning Disability'.  
Patient declines to record a specific Adjustment at this time.  
#### Pre ####
* Patient arrives at check  
* Practitioner opens GPSystem, traces & verifies demographic info (internal call to PDS)  
* Practitioner discusses RARecord with Patient  

#### Main ####
* Patient consents to record RA Flag  
  * Practitioner creates new RARecord for Patient (by recording Consent)  
  * Practitioner records Patient consented to record RA info  
    * ClientSystem captures and structures Consent information as new RARecord-Consent-1 resource  

* Patient agrees to record 'Learning Disability' as Impairment  
  * Practitioner adds Impairment from coded picklist (optionally elaborates w separate freetext)  
    * ClientSystem captures and structures Impairment information as new Impairment (CareConnect-RARecord-Condition-1) resource  
      * ClientSystem creates new CareConnect-RARecord-List-1 to reference / identify Impairment resourcesPatient declines to record any specific RAs  
  * Practitioner commits RARecord  
    * ClientSystem submits Create Consent request  
      * ServerSystem services Create Consent request  
        * ServerSystem submits Create Consent response  
    * ClientSystem submits Create List transaction request  
      * ServerSystem services Create List transaction request  
        * ServerSystem submits Create List transaction response  

## 2 Create RARecord Examples ##
### Create Consent Request ###
#### http request ####
#### body ####
#### headers ####

### Create Consent Response ###
#### http response ####
#### body ####
#### headers ####

### Create List Transaction Request ###
#### http request ####
#### body ####
#### headers ####

### Create List Transaction Response ###
#### http response ####
#### body ####
#### headers ####