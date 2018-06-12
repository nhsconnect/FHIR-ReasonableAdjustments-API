---
title: Interaction | Add
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_read.html
summary: Read operation describes interaction required to request and retrieve (and display) a Reasonable Adjustment Flag on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Read RA Record Use Case ##
### Trigger: ###
Mrs M has referral to inpatient procedure. RA Flag triggers pre-op appointment with Learning Disability Nurse N. Nurse N retrieves Mrs M's RA Record to inform discussion of her situation.

### Pre-requisites: ###
Practitioner Nrs N. logged on w SmartCard/National Identity > URPId  
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB demographic data  
### System Scope: ###
ClientSystem includes Acute/DepartmentalSystem client, SCRa, 1-click etc.  
ServerSystem includes Spine, PDS, SDS, FlagServer etc.  

### Summary: ###
Patient discusses RA need re reading difficulties; requests record RA Easy Read  
#### Pre ####
* Patient arrives at pre-op appt  
* Practitioner opens AcuteSystem, traces & verifies demographic info (internal call to PDS)  
* Practitioner opens Patient's RARecord  
  * System retrieves and displays RARecord for Patient's NHS#

#### Main ####
* Patient arrives for appointment; Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve RARecord
    * ClientSystem submits Read Consent query request (for Patient, Active, etc.)
      * ServerSystem submits Read Consent response
    * ClientSystem submits Read Flag query request (for Patient, Active, etc.)
      * ServerSystem submits Read Flag response
    * ClientSystem submits Read List query request with _included_Conditions_ (for Patient, Active, etc.)
      * ServerSystem submits Read List response

## 2 Read RA Record Examples ##
### Read Consent Request ###
#### http request ####
#### body ####
#### headers ####

### Read Consent Response ###
#### http response ####
#### body ####
#### headers ####

### Read Flag Request ###
#### http request ####
#### body ####
#### headers ####

### Read Flag Response ###
#### http response ####
#### body ####
#### headers ####

### Read List Request ###
#### http request ####
#### body ####
#### headers ####

### Read List Response ###
#### http response ####
#### body ####
#### headers ####