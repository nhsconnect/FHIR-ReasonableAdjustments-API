---
title: Interaction | Update
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_update_remix.html
summary: Update operation describes interaction required to update a Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Update RA Record Use Case ##
### 1.1 Trigger: ####
Post-op appt with GP. Patient requests change of 'Easy Read' Adjustment to 'Large Print'
### 1.2 Pre-requisites: ####
(This scenario assumes someone has created an 'Easy Read' Reasonable Adjustment between the Read and Update examples)  
Practioner Dr D. logged on w SmartCard/National Identity > URPId - see [API Security](design_security.html)  
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB demographic data - see [Patient Demographics](design_demographics.html)  
ClientSystem has Patient's existing RArecord available - see ['Read an RA Flag'](design_operations_read.html)  
### 1.3 System Scope: ####
ClientSystem includes GPSystem client, SCRa, 1-click etc.  
ServerSystem includes Spine, PDS, SDS, FlagServer etc.  
### 1.4 Summary: 
During appt GP discusses RA Record. Patient requests change of Reasonable Adjustment 'Easy Read' to 'Large Print'.  
Practitioner updates (soft deletes) existing 'Easy Read' Adjustment, records Removal reason 'Entered in error'  
[then creates new 'Large Print' Adjustment - not shown cf. Create Consent response].  

#### Pre ####
Patient arrives at post-op appt
Practitioner opens GPSystem, traces & verifies demographic info (internal call to PDS)
Practitioner opens Patient's RARecord
  System retrieves and displays RARecord for Patient's NHS
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
  * _[not shown cf. Create Consent request & response](design_operations_create.html#create-consent-or-flag-resource) as a directly analogous operation etc..._

## 2 Update RA Record Examples ##
### 2.1 Update Flag Request ####
#### http request ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a HTTP/1.1
If-Match: W/"25777f7d-27bc"
```
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-UpdateFlagRequestBody-example.xml"
title="RARecord-UpdateFlagRequestBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-UpdateFlagRequestBody-example.json"
title="RARecord-UpdateFlagRequestBody-example"
type="json" %}
{% include custom/fhir.header.html %}
In addition, updates MUST include the If-Match header specifying the version of the resource they are updating.

### 2.2 Update Flag Response ####
{% include custom/fhir.response.html %}  
Edge cases TBD and detailed during development
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-UpdateFlagResponseBody-example.xml"
title="RARecord-UpdateFlagResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-UpdateFlagResponseBody-example.json"
title="RARecord-UpdateFlagResponseBody-example"
type="json" %}
{% include custom/fhir.header.html %}
