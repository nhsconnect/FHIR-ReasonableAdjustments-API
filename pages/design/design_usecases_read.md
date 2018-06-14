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
#### 1.1 Trigger: ####
Mrs M has referral to inpatient procedure. RA Flag triggers pre-op appointment with Learning Disability Nurse N. Nurse N retrieves Mrs M's RA Record to inform discussion of her situation.

#### 1.2 Pre-requisites: ####
Practitioner Nrs N. logged on w SmartCard/National Identity > URPId  
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB demographic data  
#### 1.3 System Scope: ####
ClientSystem includes Acute/DepartmentalSystem client, SCRa, 1-click etc.  
ServerSystem includes Spine, PDS, SDS, FlagServer etc.  

#### 1.4 Summary: ####
Patient discusses RA need re reading difficulties; requests record RA Easy Read  
#### Pre ####
* Patient arrives at pre-op appt  
* Practitioner opens AcuteSystem, traces & verifies demographic info (internal call to PDS)  
* Practitioner opens Patient's RARecord  
  * System retrieves and displays RARecord for Patient's NHS

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
#### 2.1 Read Consent Request ####
#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/flagserver/Consent?
  patient=999999998&status=active&category=RAFlag HTTP/1.1
```
#### body ####
N/A
#### headers ####

#### 2.2 Read Consent Response ####
#### http response ####
TBD but 200 OK on successful read etc.
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadConsentResponseBody-example.xml"
title="RARecord-ReadConsentResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadConsentResponseBody-example.json"
title="RARecord-ReadConsentResponseBody-example"
type="json" %}
#### headers ####

#### 2.3 Read Flag Request ####
#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/flagserver/Flag?
  patient=999999998&status=active&category=RAFlag HTTP/1.1
```
#### body ####
N/A
#### headers ####

#### 2.4 Read Flag Response ####
#### http response ####
TBD but 200 OK on successful read etc.
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody-example.xml"
title="RARecord-ReadFlagResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody-example.json"
title="RARecord-ReadFlagResponseBody-example"
type="json" %}
#### headers ####

#### 2.5 Read List Request ####
#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/flagserver/List?
  subject=999999998&clinicalStatus=current&code=1094391000000102
  &_include=List:item.clinicalStatus=active
```
#### body ####
N/A
#### headers ####

#### 2.6 Read List Response ####
#### http response ####
TBD but 200 OK on successful read etc.
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadListResponseBody-example.xml"
title="RARecord-ReadListResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadListResponseBody-example.json"
title="RARecord-ReadListResponseBody-example"
type="json" %}
#### headers ####