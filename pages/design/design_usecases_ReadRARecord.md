---
title: Use Case | Read RA Record
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_ReadRARecord.html
summary: Description of use case on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Read RA Record ##

#### Trigger: ####
* Mrs M is referred to an inpatient procedure.  
* Presence of RA Flag triggers pre-operation appointment with Learning Disability Nurse N.  
* Nurse N retrieves Mrs M's RA Record to inform discussion of her situation.  

#### System Scope: ####
* ClientSystem includes Acute/DepartmentalSystem client, SCRa, 1-click etc.  
* ServerSystem includes Spine, PDS, SDS, FlagServer etc.  

#### Summary: ####
Patient has an RA Flag; Practitioner requests record.

#### Pre ####
* Patient arrives at pre-operation appointment  
* Practitioner Nrs N. is logged on with SmartCard/National Identity  
  * Gives User Role Profile Identifier (URPId)  
* Patient Mrs M. has been PDS Traced  
  * Gives verified NHS#, Name, DoB demographic data  

#### Main ####
* Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve RARecord
    * ClientSystem submits Read Consent request [(xml)](design_usecases_ReadRARecord.html#21-read-consent-request---xml-example) [(json)](design_usecases_ReadRARecord.html#22-read-consent-request---json-example)
      * ServerSystem submits Read Consent response [(xml)](design_usecases_ReadRARecord.html#23-read-consent-response---xml-example) [(json)](design_usecases_ReadRARecord.html#24-read-consent-response---json-example)
    * ClientSystem submits Read Flag request [(xml)](design_usecases_ReadRARecord.html#25-read-flag-request---xml-example) [(json)](design_usecases_ReadRARecord.html#26-read-flag-request---json-example)
      * ServerSystem submits Read Flag response [(xml)](design_usecases_ReadRARecord.html#27-read-flag-response---xml-example) [(json)](design_usecases_ReadRARecord.html#28-read-flag-response---json-example) - examples provided for 0, 1 and 2 Flags found in searchset
    * ClientSystem submits Read List request [(xml)](design_usecases_ReadRARecord.html#29-read-list-request---xml-example) [(json)](design_usecases_ReadRARecord.html#210-read-list-request---json-example)
      * ServerSystem submits Read List response [(xml)](design_usecases_ReadRARecord.html#211-read-list-response---xml-example) [(json)](design_usecases_ReadRARecord.html#212-read-list-response---json-example)


---

## 2 Interaction Examples ##

Examples of http requests, responses and payloads

### 2.1 Read Consent Request - xml example ###
#### http request & headers ####
``` http
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.read:1
```

#### http body ####
**None**

### 2.2 Read Consent Request - json example ###
#### http request & headers ####
``` http
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=json HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.read:1
```

#### http body ####
**None**

### 2.3 Read Consent Response - xml example ###
#### http response & headers ####
``` http
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 11:00:00 GMT
Content-Type: application/fhir+xml
```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadConsentResponseBody-example.xml"
title="Read Consent Response"
type="xml" %}

### 2.4 Read Consent Response - json example ###
#### http response & headers ####
``` http
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 11:00:00 GMT
Content-Type: application/fhir+json
```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadConsentResponseBody-example.json"
title="Read Consent Response"
type="json" %}

### 2.5 Read Flag Request - xml example ###
#### http request & headers ####
``` http
GET https://clinicals.spineservices.nhs.uk/STU3/Flag?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.read:1
```

#### http body ####
**None**

### 2.6 Read Flag Request - json example ###
#### http request & headers ####
``` http
GET https://clinicals.spineservices.nhs.uk/STU3/Flag?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=json HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.read:1
```

#### http body ####
**None**

### 2.7 Read Flag response - xml example ###
#### http response & headers ####
``` http
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 11:00:01 GMT
Content-Type: application/fhir+xml
```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody-example.xml"
title="Read Flag response (0 Flag)"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody1Flag.xml"
title="Read Flag response (1 Flag)"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody2Flags.xml"
title="Read Flag response (2 Flags)"
type="xml" %}

### 2.8 Read Flag response - json example ###
#### http response & headers ####
``` http
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 11:00:01 GMT
Content-Type: application/fhir+json
```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody-example.json"
title="Read Flag response (0 Flag)"
type="json" %}

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody1Flag.json"
title="Read Flag response (1 Flag)"
type="json" %}

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadFlagResponseBody2Flags.json"
title="Read Flag response (2 Flags)"
type="json" %}

### 2.9 Read List request - xml example ###
#### http request & headers ####
``` http
GET https://clinicals.spineservices.nhs.uk/STU3/List?
 patient=999999998&
 status=current&
 code=http://snomed.info/sct|1094391000000102&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.read:1

```

#### http body ####
**None**

### 2.10 Read List request - json example ###
#### http request & headers ####
``` http
GET https://clinicals.spineservices.nhs.uk/STU3/List?
 patient=999999998&
 status=current&
 code=http://snomed.info/sct|1094391000000102&
 _format=json HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.read:1

```

#### http body ####
**None**

### 2.11 Read List response - xml example ###
#### http response & headers ####
``` http
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 11:00:01 GMT
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadListResponseBody-example.xml"
title="Read List response"
type="xml" %}

### 2.12 Read List response - json example ###
#### http response & headers ####
``` http
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 11:00:01 GMT
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-ReadListResponseBody-example.json"
title="Read List response"
type="json" %}

      
---
