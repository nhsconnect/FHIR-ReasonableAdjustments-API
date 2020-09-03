---
title: Use Case | Update Adjustment
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_UpdateAdjustment.html
summary: Description of use case on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Update Adjustment ##

####  Trigger: ####
Post-operative appointment with GP. Patient requests change of 'Easy Read' Adjustment to 'Large Print'

####  System Scope: ####
ClientSystem includes GPSystem client, SCRa, 1-click etc.  
ServerSystem includes Spine, PDS, SDS, FlagServer etc.  

####  Summary: ####
During appointment GP discusses RA Record, Patient requests change of Reasonable Adjustment 'Easy Read' to 'Large Print'.  
Practitioner updates (soft deletes) existing 'Easy Read' Adjustment, records Removal reason 'Entered in error'  
Practitioner creates new 'Large Print' Adjustment.  

#### Pre ####

* Practitioner logged into ClientSystem, traces & verifies demographic info
* Practitioner opens Patient's RARecord
  * System retrieves and displays RARecord for Patient's NHS

* Practitioner discusses RARecord and RA with Patient, Patient doesn't like Easy Read
* Practitioner discusses options w Patient, Patient agrees change RA 'Easy Read' to 'Large Print'

#### Main ####

* Practitioner removes (soft deletes) existing 'Easy Read' Adjustment, records Removal reason 'Entered in error' and supporting comment;
  * ClientSystem updates client-side Flag resource

* Practitioner commits RARecord
  * ClientSystem submits Update Flag request [(xml)](design_usecases_UpdateAdjustment.html#21-update-flag-request---xml-example) [(json)](design_usecases_UpdateAdjustment.html#22-update-flag-request---json-example)
    * ServerSystem submits Update Flag response [(xml)](design_usecases_UpdateAdjustment.html#23-update-flag-response---xml-example) [(json)](design_usecases_UpdateAdjustment.html#24-update-flag-response---json-example)

* Practitioner records new 'Large Print' Adjustment
  * ClientSystem captures and structures Adjustment information as new RARecord-Flag-1 resource 
* Practitioner commits RARecord
  * ClientSystem submits Create Flag request [(xml)](design_usecases_UpdateAdjustment.html#25-create-flag-request---xml-example) [(json)](design_usecases_UpdateAdjustment.html#26-create-flag-request---json-example)
    * ServerSystem submits Create Flag response [(xml)](design_usecases_UpdateAdjustment.html#27-create-flag-response---xml-example) [(json)](design_usecases_UpdateAdjustment.html#28-create-flag-response---json-example)

## 2 Interaction Examples ##

Examples of http requests, responses and payloads

### 2.1 Update Flag Request - xml example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Flag/2acb0536-0a8f-48c9-8a2f-6ee82860f186 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1
If-Match: W/"aa755bd6-2be9-4971-972a-6724879c5cb1"


```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-UpdateFlagRequest.xml"
title="Update Flag Request"
type="xml" %}

### 2.2 Update Flag Request - json example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Flag/2acb0536-0a8f-48c9-8a2f-6ee82860f186 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1
If-Match: W/"aa755bd6-2be9-4971-972a-6724879c5cb1"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-UpdateFlagRequest.json"
title="Update Flag Request"
type="json" %}

### 2.3 Update Flag Response - xml example ###

#### http request & headers ####
```
HTTP/1.1 200 OK
Date: Thur, 25 Jul 2018 11:00:00 GMT
Last-Modified: 2018-07-25T11:00:00+00:00
ETag: W/"b0c4bd5f-6133-4ac4-af48-82570ad15007”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-UpdateFlagResponse.xml"
title="Update Flag Response"
type="xml" %}

### 2.4 Update Flag Response - json example ###

#### http request & headers ####
```
HTTP/1.1 200 OK
Date: Thur, 25 Jul 2018 11:00:00 GMT
Last-Modified: 2018-07-25T11:00:00+00:00
ETag: W/"b0c4bd5f-6133-4ac4-af48-82570ad15007”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-UpdateFlagResponse.json"
title="Update Flag Response"
type="json" %}

### 2.5 Create Flag Request - xml example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-CreateFlagRequest.xml"
title="Create Flag Request"
type="xml" %}

### 2.6 Create Flag Request - json example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-CreateFlagRequest.json"
title="Create Flag Request"
type="json" %}

### 2.7 Create Flag Response - xml example ###

#### http request & headers ####
```
HTTP/1.1 201 Created
Date: Thu, 25 Jul 2018 11:03:00 GMT
Last-Modified:2018-07-25T11:03:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Flag/d82888a3-1584-4e7f-99f1-3e578a1c9d37/_history/5b293b55-5ca5-4670-91e2-adb905001b96
ETag: W/"5b293b55-5ca5-4670-91e2-adb905001b96”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-CreateFlagResponse.xml"
title="Create Flag Response"
type="xml" %}

### 2.8 Create Flag Response - json example ###

#### http request & headers ####
```
HTTP/1.1 201 Created
Date: Thu, 25 Jul 2018 11:03:00 GMT
Last-Modified:2018-07-25T11:03:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Flag/d82888a3-1584-4e7f-99f1-3e578a1c9d37/_history/5b293b55-5ca5-4670-91e2-adb905001b96
ETag: W/"5b293b55-5ca5-4670-91e2-adb905001b96”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-CreateFlagResponse.json"
title="Create Flag Response"
type="json" %}

---
---