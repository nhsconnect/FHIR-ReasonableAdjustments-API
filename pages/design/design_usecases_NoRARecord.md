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

### 2.1 Read Consent request ###

#### http request & headers ####
{% include codetags.html xml="GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.11
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.read:1"
json="GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=json HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.read:1" %}

#### http body ####
**None**

### 2.2 Read Consent response ###

#### http response & headers ####

{% include codetags.html xml="HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 10:00:00 GMT
Content-Type: application/fhir+xml
"
json="HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 10:00:00 GMT
Content-Type: application/fhir+json" %}

#### http body ####
{% include codetags.html title="Read Fail Empty Bundle" xmlpath="usecaseexamples/ReadFailEmptyBundle.xml" jsonpath="usecaseexamples/ReadFailEmptyBundle.json" %}

