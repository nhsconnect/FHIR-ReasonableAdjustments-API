---
title: Use Case | Create RA Record
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_CreateRARecord.html
summary: Description of use case on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Create RA Record ##

#### Trigger: ####
* GP initiates Reasonable Adjustment Flag discussion at annual health check 

#### System Scope: ####
* ClientSystem includes Acute/DepartmentalSystem client, SCRa, 1-click etc.  
* ServerSystem includes Spine, PDS, SDS, FlagServer etc.  

#### Summary: ####
Practitioner creates RARecord, recording Consent from Patient and that Impairment is 'Learning Disability'.  
Patient declines to record a specific Adjustment at this time.  

#### Pre ####
* Patient arrives at check  
* Practitioner logged into ClientSystem, traces & verifies demographic information
* Practitioner searches for Patient's RARecord
  * ClientSystem searched and failed to find existing RARecord [(see Use Case Initial Read Failure)](/design_usecases_NoRARecord.html#1-no-ra-record)
* Practitioner discusses RARecord with Patient  

#### Main ####
* Patient consents to record RA Flag  
  * Practitioner creates new RARecord for Patient (by recording Consent)  
  * Practitioner records Patient consented to record RA info  
    * ClientSystem captures and structures Consent information as new RARecord Consent-1 resource [(xml)](design_usecases_CreateRARecord.html#21-create-consent-resource---xml-example) [(json)](design_usecases_CreateRARecord.html#22-create-consent-resource---json-example)
* Patient agrees to record 'Learning Disability' as Impairment  
  * Practitioner adds Impairment from coded picklist (optionally elaborates w separate freetext)  
    * ClientSystem captures and structures Impairment information as new Impairment (CareConnect-RARecord-Condition-1) resource [(xml)](design_usecases_CreateRARecord.html#23-create-condition-resource---xml-example) [(json)](design_usecases_CreateRARecord.html#24-create-condition-resource---json-example)

* Patient declines to record any specific Adjustments at this time

* Practitioner commits RARecord  
    * ClientSystem submits Create Consent request [(xml)](design_usecases_CreateRARecord.html#25-create-consent-request---xml-example) [(json)](design_usecases_CreateRARecord.html#26-create-consent-request---json-example)
      * ServerSystem submits Create Consent response [(xml)](design_usecases_CreateRARecord.html#27-create-consent-response---xml-example) [(json)](design_usecases_CreateRARecord.html#28-create-consent-response---json-example)

    * ClientSystem captures and structures Provenance information as new Provenance (RARecord-Provenance-1) resource [(xml)](design_usecases_CreateRARecord.html#29-create-provenance-resource---xml-example) [(json)](design_usecases_CreateRARecord.html#210-create-provenance-resource---json-example)
    * ClientSystem creates new CareConnect-RARecord-List-1 to contain Impairment resource [(xml)](design_usecases_CreateRARecord.html#211-create-list-resource---xml-example) [(json)](design_usecases_CreateRARecord.html#212-create-list-resource---json-example)
    * ClientSystem contains new Impairment resource within CareConnect-RARecord-List-1 resource
    * ClientSystem contains new Provenance resource within CareConnect-RARecord-List-1 resource [(xml)](design_usecases_CreateRARecord.html#213-create-list-condition-resource---xml-example) [(json)](design_usecases_CreateRARecord.html#214-create-list-condition-resource---json-example)
    * ClientSystem submits Create Condition request [(xml)](design_usecases_CreateRARecord.html#215-create-list-condition-request---xml-example) [(json)](design_usecases_CreateRARecord.html#216-create-list-condition-request---json-example)
      * ServerSystem submits Create Condition response [(xml)](design_usecases_CreateRARecord.html#217-create-list-condition-response---xml-example) [(json)](design_usecases_CreateRARecord.html#218-create-list-condition-response---json-example)

---


## 2 Examples ##

Examples of resources http requests, responses and payloads

### 2.1 Create Consent Resource - xml example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConsentRequest.xml"
title="Create Consent Resource"
type="xml" %}

### 2.2 Create Consent Resource - json example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConsentRequest.json"
title="Create Consent Resource"
type="json" %}

### 2.3 Create Condition Resource - xml example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConditionRequest.xml"
title="Create Condition Resource"
type="xml" %}

### 2.4 Create Condition Resource - json example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConditionRequest.json"
title="Create Condition Resource"
type="json" %}

### 2.5 Create Consent Request - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Consent HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 0fd9c402-3bca-48a4-a5c3-06c5dd064a76
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConsentRequest.xml"
title="Create Consent Request"
type="xml" %}


### 2.6 Create Consent Request - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Consent HTTP/1.1
Authorization:Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 0fd9c402-3bca-48a4-a5c3-06c5dd064a76
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConsentRequest.json"
title="Create Consent Request"
type="json" %}


### 2.7 Create Consent Response - xml example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Consent/f1dc0ac6-45ff-4d2b-bf91-793971e3e286/_history/cccacb16-e087-45ee-8ddd-5fbd6223e5a2
ETag: W/"cccacb16-e087-45ee-8ddd-5fbd6223e5a2”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConsentResponse.xml"
title="Create Consent Response"
type="xml" %}


### 2.8 Create Consent Response - json example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: [resourceURL]
ETag: W/"resourceVID”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConsentResponse.json"
title="Create Consent Response"
type="json" %}

### 2.9 Create Provenance Resource - xml example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateProvenanceResource.xml"
title="Create Provenance Resource"
type="xml" %}

### 2.10 Create Provenance Resource - json example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create Provenance Resource"
type="json" %}

### 2.11 Create List Resource - xml example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateListResource.xml"
title="Create List Resource"
type="xml" %}

### 2.12 Create List Resource - json example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create List Resource"
type="json" %}

### 2.13 Create List Condition Resource - xml example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-ListConditionResource.xml"
title="Create List Condition Resource"
type="xml" %}

### 2.14 Create List Condition Resource - json example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create List Condition Resource"
type="json" %}

### 2.15 Create List Condition Request - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/List HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 0fd9c402-3bca-48a4-a5c3-06c5dd064a76
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-ListConditionResource.xml"
title="Create List Condition Request"
type="xml" %}


### 2.16 Create List Condition Request - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/List HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 0fd9c402-3bca-48a4-a5c3-06c5dd064a76
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create List Condition Request"
type="json" %}


### 2.17 Create List Condition Response - xml example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/List/130f416a-055d-4a5d-a453-2b7c2de3b57b/_history/f2fef5e5-c38a-408c-a9bc-2d49923928f8
ETag: W/"f2fef5e5-c38a-408c-a9bc-2d49923928f8”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-ListConditionResponse.xml"
title="Create List Condition Response"
type="xml" %}


### 2.18 Create List Condition Response - json example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/List/130f416a-055d-4a5d-a453-2b7c2de3b57b/_history/f2fef5e5-c38a-408c-a9bc-2d49923928f8
ETag: W/"f2fef5e5-c38a-408c-a9bc-2d49923928f8”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create List Condition Response"
type="json" %}


