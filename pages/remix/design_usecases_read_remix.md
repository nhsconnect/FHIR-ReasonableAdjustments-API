---
title: Interaction | Read
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_read_remix.html
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
Patient has a RA Flag; Practitioner requests record
#### Pre ####
* Patient arrives at pre-op appt  
* Practitioner opens AcuteSystem, traces & verifies demographic info (internal call to PDS)  
* Practitioner opens Patient's RARecord  
  * System retrieves and displays RARecord for Patient's NHS

#### Main ####
* Patient arrives for appointment; Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve RARecord
    * ClientSystem submits Read Consent request (for Patient, Active, etc.)
      * ServerSystem submits Read Consent response
    * ClientSystem submits Read Flag request (for Patient, Active, etc.)
      * ServerSystem submits Read Flag response
    * ClientSystem submits Read List request with _included_Conditions_ (for Patient, Active, etc.)
      * ServerSystem submits Read List response

## 2 Read RA Record Use Case Examples ##
## 2.1 Read Consent Request ##
#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
  patient=999999998&status=active&category=RAFlag HTTP/1.1
```
#### body ####
N/A
{% include custom/fhir.header.html %}

## 2.2 Read Consent Response ##
{% include custom/fhir.response.html %}  
Edge cases TBD and detailed during development
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadConsentResponseBody-example.xml"
title="RARecord-ReadConsentResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadConsentResponseBody-example.json"
title="RARecord-ReadConsentResponseBody-example"
type="json" %}
{% include custom/fhir.header.html %}

## 2.3 Read Flag Request ##

#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Flag?
  patient=999999998&status=active&category=RAFlag HTTP/1.1
```
#### body ####
N/A
{% include custom/fhir.header.html %}

## 2.4 Read Flag Response ##

Two variants are presented
- 1. Where no Adjustments have been recorded
- 2. Where 2 Adjustments have been recorded

The Requests remain the same, Responses differ.

## 2.4.1 Empty Searchset ##

Assumes direct follow on from the scenario presented in 'Create an RA Flag' i.e. no specific Adjustments are recorded yet, and default Considertion banners will be displayed.

{% include custom/fhir.response.html %}  
Edge cases TBD and detailed during development
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody-example.xml"
title="RARecord-ReadFlagResponseBody-example-2"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody-example.json"
title="RARecord-ReadFlagResponseBody-example-2"
type="json" %}
{% include custom/fhir.header.html %}

## 2.4.2 Multiple result Searchset ##

Assumes that prior to this scenario 2 Adjustments have been recorded on behalf of the Patient.  
Here, the Adjustments are:
- Communication adjustment: Provide written reminders and advice
- Communication adjustment: Adjust for use of communication book / aid

{% include custom/fhir.response.html %}  
Edge cases TBD and detailed during development
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody-example-2.xml"
title="RARecord-ReadFlagResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody-example-2.json"
title="RARecord-ReadFlagResponseBody-example"
type="json" %}
{% include custom/fhir.header.html %}

## 2.5 Read List Request ##
#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
  subject=999999998&clinicalStatus=current&code=1094391000000102
  &_include=List:item.clinicalStatus=active
```
#### body ####
N/A
{% include custom/fhir.header.html %}

## 2.6 Read List Response ##
{% include custom/fhir.response.html %}  
Edge cases TBD and detailed during development
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadListResponseBody-example.xml"
title="RARecord-ReadListResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadListResponseBody-example.json"
title="RARecord-ReadListResponseBody-example"
type="json" %}
{% include custom/fhir.header.html %}