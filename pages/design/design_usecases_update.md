---
title: Interaction | Update
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_update.html
summary: Update operation describes interaction required to update a Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Update RA Record Use Case ##
### Trigger: ###
Post-op appt with GP. Patient requests change of 'Easy Read' Adjustment to 'Large Print'
### Pre-requisites: ###
(This scenario assumes someone has created an 'Easy Read' Reasonable Adjustment between the Read and Update examples)  
Practioner Dr D. logged on w SmartCard/National Identity > URPId  
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB demographic data  
ClientSystem has Patient's existing RArecord available - see ['Read an RA Flag'](https://nhsconnect.github.io/FHIR-ReasonableAdjustments-API/~)
### System Scope: ###
ClientSystem includes GPSystem client, SCRa, 1-click etc.  
ServerSystem includes Spine, PDS, SDS, FlagServer etc.  
### Summary: #
During appt GP discusses RA Record. Patient requests change of Reasonable Adjustment 'Easy Read' to 'Large Print'.  
Practitioner updates (soft deletes) existing 'Easy Read' Adjustment, records Removal reason 'Entered in error'  
[then creates new 'Large Print' Adjustment - not shown cf. Create Consent response].  

#### Pre ####
Patient arrives at post-op appt
Practitioner opens GPSystem, traces & verifies demographic info (internal call to PDS)
Practitioner opens Patient's RARecord
  System retrieves and displays RARecord for Patient's NHS#
#### Main ####
* Practitioner discusses RARecord and RA with Patient, Patient doesn't like Easy Read
* Practitioner discusses options w Patient, Patient agrees change RA 'Easy Read' to 'Large Print'
* Practitioner updates (soft deletes) existing 'Easy Read' Adjustment, records Removal reason 'Entered in error';
  * ClientSystem updates held Flag resource
* Practitioner commits RARecord
  * ClientSystem submits Update Flag request
    * ServerSystem services Update Consent request
      * ServerSystem submits Update Consent response
* _Practitioner records new 'Large Print' Adjustment_
  * _ClientSystem captures and structures Adjustment information as new RARecord-Flag-1 resource_
  * _..._
  * _[not shown cf. Create Consent request & response](https://nhsconnect.github.io/FHIR-ReasonableAdjustments-API/~) as a directly analogous operation etc..._

## 2 Update RA Record Examples ##
### Update Flag Request ###
#### http request ####
#### body ####
#### headers ####

### Update Flag Response ###
#### http response ####
#### body ####
#### headers ####
