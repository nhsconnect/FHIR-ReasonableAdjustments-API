---
title: Interaction | Read
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_read_remix.html
summary: Read operation describes interaction required to request and retrieve (and display) a Reasonable Adjustment Flag on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Read RA Record ##

#### Trigger: ####
* Mrs M has referral to an inpatient procedure.  
* Presence of RA Flag triggers pre-operation appointment with Learning Disability Nurse N.  
* Nurse N retrieves Mrs M's RA Record to inform discussion of her situation.  

#### System Scope: ####
* ClientSystem includes Acute/DepartmentalSystem client, SCRa, 1-click etc.  
* ServerSystem includes Spine, PDS, SDS, FlagServer etc.  

#### Summary: ####
Patient has a RA Flag; Practitioner requests record.

#### Pre ####
* Patient arrives at pre-operation appointment  
* Practitioner Nrs N. is logged on with SmartCard/National Identity  
  * => URPId  
* Patient Mrs M. has been PDS Traced  
  * => verified NHS#, Name, DoB demographic data  

#### Main ####
* Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve RARecord
    * ClientSystem submits Read Consent request [(xml)](design_usecases_read_remix.html#21-read-consent-request---xml-example) [(json)](design_usecases_remix.html#22-read-consent-request---json-example)
      * ServerSystem submits Read Consent response [(xml)](design_usecases_read_remix.html#23-read-consent-response---xml-example) [(json)](design_usecases_remix.html#24-read-consent-response---json-example)
    * ClientSystem submits Read Flag request [(xml)](design_usecases_read_remix.html#25-read-flag-request---xml-example) [(json)](design_usecases_remix.html#26-read-flag-request---json-example)
      * ServerSystem submits Read Flag response [(xml)](design_usecases_read_remix.html#27-read-flag-response---xml-example) [(json)](design_usecases_remix.html#28-read-flag-response---json-example)
    * ClientSystem submits Read List request [(xml)](design_usecases_read_remix.html#29-read-list-request---xml-example) [(json)](design_usecases_remix.html#210-read-list-request---json-example)
      * ServerSystem submits Read List response [(xml)](design_usecases_read_remix.html#211-read-list-response---xml-example) [(json)](design_usecases_read_remix.html#212-read-list-response---json-example)
    * ClientSystem submits Read Conditions request [(xml)](design_usecases_read_remix.html#213-read-conditions-request---xml-example) [(json)](design_usecases_read_remix.html#214-read-conditions-request---json-example)
      * ServerSystem submits Read Conditions response [(xml)](design_usecases_read_remix.html#215-read-conditions-response---xml-example) [(json)](design_usecases_read_remix.html#216-read-conditions-response---json-example)

---
### 2.1 Read Consent request - xml example ###
#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:consent:read

```

#### http body ####
**None**

### 2.2 Read Consent request - json example ###
#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=json HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:consent:read

```

#### http body ####
**None**

### 2.3 Read Consent response - xml example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-24T11:00:00+00:00
ETag: W/"bundleUUID”
Content-Type:application/xml+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Read Consent response"
type="xml" %}

### 2.4 Read Consent response - json example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-24T10:00:00+00:00
ETag: W/"bundleUUID”
Content-Type:application/json+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Read Consent response"
type="json" %}

### 2.5 Read Flag request - xml example ###
#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Flag?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:flag:read

```

#### http body ####
**None**

### 2.6 Read Flag request - json example ###
#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Flag?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=json HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:flag:read

```

#### http body ####
**None**

### 2.7 Read Flag response - xml example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 11:00:01 GMT
Last-Modified:2018-07-24T11:00:01+00:00
ETag: W/"bundleUUID”
Content-Type:application/xml+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Read Flag response"
type="xml" %}

### 2.8 Read Flag response - json example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 11:00:01 GMT
Last-Modified:2018-07-24T11:00:01+00:00
ETag: W/"bundleUUID”
Content-Type:application/json+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Read Flag response"
type="json" %}

### 2.9 Read List request - xml example ###
#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
 patient=999999998&
 status=current&
 code=http://snomed.info/sct|1094391000000102&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:list:read

```

#### http body ####
**None**

### 2.10 Read List request - json example ###
#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
 patient=999999998&
 status=current&
 code=http://snomed.info/sct|1094391000000102&
 _format=json HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:list:read

```

#### http body ####
**None**

### 2.11 Read List response - xml example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 11:00:01 GMT
Last-Modified:2018-07-24T11:00:02+00:00
ETag: W/"bundleUUID”
Content-Type:application/xml+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Read List response"
type="xml" %}

### 2.12 Read List response - json example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 11:00:01 GMT
Last-Modified:2018-07-24T11:00:02+00:00
ETag: W/"bundleUUID”
Content-Type:application/json+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Read List response"
type="json" %}

### 2.13 Read Conditions request - xml example ###
#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Condition?
 _list=4c8d19af-7755-4954-93df-93c964ddf349&
 clinical-status=active&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:condition:read

```

#### http body ####
**None**

### 2.14 Read Conditions request - json example ###
#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Condition?
 _list=4c8d19af-7755-4954-93df-93c964ddf349&
 clinical-status=active&
 _format=json HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:condition:read

```

#### http body ####
**None**

### 2.15 Read Conditions response - xml example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 11:00:01 GMT
Last-Modified:2018-07-24T11:00:03+00:00
ETag: W/"bundleUUID”
Content-Type:application/xml+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Read Conditions response"
type="xml" %}

### 2.16 Read Conditions response - json example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 11:00:01 GMT
Last-Modified:2018-07-24T11:00:01+00:00
ETag: W/"bundleUUID”
Content-Type:application/json+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Read Conditions response"
type="json" %}


      
---
      
## 2 Read RA Record Use Case Examples ##

### 2.1 Read Consent Request ###
#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
  patient=999999998&status=active&category=RAFlag HTTP/1.1
```
#### body ####
N/A
{% include custom/fhir.header.html %}

### 2.2 Read Consent Response ###
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

### 2.3 Read Flag Request ###

#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Flag?
  patient=999999998&status=active&category=RAFlag HTTP/1.1
```
#### body ####
N/A
{% include custom/fhir.header.html %}

### 2.4 Read Flag Response ###

Two variants are presented
- 1. Where no Adjustments have been recorded
- 2. Where 2 Adjustments have been recorded

The Requests remain the same, Responses differ.

### 2.4.1 Empty Searchset ###

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

### 2.4.2 Multiple result Searchset ###

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

### 2.5 Read List Request ###
#### http request ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
  subject=999999998&clinicalStatus=current&code=1094391000000102
  &_include=List:item.clinicalStatus=active
```
#### body ####
N/A
{% include custom/fhir.header.html %}

### 2.6 Read List Response ###
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