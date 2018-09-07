---
title: Use Case | No RA Record
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_NoRARecord.html
summary: Description of use case on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 No RA Record ##


#### Pre ####
* Practitioner logged into ClientSystem, traces & verifies demographic info - see [API Security](design_security.html)

#### Main ####
* Practitioner searches for Patient's RARecord
  * ClientSystem searched and failed to find existing RARecord
    * ClientSystem submits Read Consent request (for Patient, Active, etc.) [(xml)](design_usecases_NoRARecord.html#21-read-consent-request---xml-example) [(json)](design_usecases_NoRARecord.html#22-read-consent-request---json-example)
    * ServerSystem submits Read Consent response [(xml)](design_usecases_NoRARecord.html#23-read-consent-response---xml-example) [(json)](design_usecases_NoRARecord.html#24-read-consent-response---json-example)

## 2 Interaction Examples ##

### 2.1 Read Consent request - xml example  ###

#### http request & headers ####

```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.read:1

```

#### http body ####
**None**

### 2.2 Read Consent request - json example  ###

#### http request & headers ####

```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=json HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.read:1

```

#### http body ####
**None**

### 2.3 Read Consent response - xml example ###

#### http response & headers ####
```
HTTP/1.1 404 NOT FOUND
Date: Tue, 24 Jul 2018 10:00:00 GMT
Content-Type: application/fhir+xml

```
**DQ:** Would you use full header & metadata in a failure OperationOutcome response?  
**DN:** Can't see why you would.  
From FHIR spec, 'The resource is not designed to be persisted or referenced from other parts of the workflow.'  
Therefore it won't have a versionId/ETag, lastModified would only ever be the same as Date, no Location as not persisted.
Failure response therefore drops to minimal Date, Content-Type headers.
#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/ReadFailOperationOutcome.xml"
title="Read Fail Operation Outcome"
type="xml" %}

### 2.4 Read Consent response - json example ###

#### http response & headers ####
```
HTTP/1.1 404 PATIENT NOT FOUND
Date: Tue, 24 Jul 2018 10:00:00 GMT
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/ReadFailOperationOutcome.json"
title="Read Fail Operation Outcome"
type="json" %}