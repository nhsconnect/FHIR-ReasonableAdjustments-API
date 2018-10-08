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
    * ClientSystem captures and structures Consent information as new RARecord-Consent-1 resource [(xml)](design_usecases_CreateRARecord.html#21-new-consent-resource---xml-example) [(json)](design_usecases_CreateRARecord.html#22-new-consent-resource---json-example)

* Patient agrees to record 'Learning Disability' as Impairment  
  * Practitioner adds Impairment from coded picklist (optionally elaborates w separate freetext)  
    * ClientSystem captures and structures Impairment information as new Impairment (CareConnect-RARecord-Condition-1) resource [(xml)](design_usecases_CreateRARecord.html#23-new-impairment-resource---xml-example) [(json)](design_usecases_CreateRARecord.html#24-new-impairment-resource---json-example)

* Patient declines to record any specific Adjustments at this time

* Practitioner commits RARecord  
    * ClientSystem submits Create Consent request [(xml)](design_usecases_CreateRARecord.html#31-create-consent-request---xml-example) [(json)](design_usecases_CreateRARecord.html#32-create-consent-request---json-example)
      * ServerSystem submits Create Consent response [(xml)](design_usecases_CreateRARecord.html#33-create-consent-response---xml-example) [(json)](design_usecases_CreateRARecord.html#34-create-consent-response---json-example)
    * ClientSystem submits Create Condition request [(xml)](design_usecases_CreateRARecord.html#35-create-condition-request---xml-example) [(json)](design_usecases_CreateRARecord.html#36-create-condition-request---json-example)
      * ServerSystem submits Create Condition response [(xml)](design_usecases_CreateRARecord.html#37-create-condition-response---xml-example) [(json)](design_usecases_CreateRARecord.html#38-create-condition-response---json-example)
        * ClientSystem creates new CareConnect-RARecord-List-1 to reference / identify Impairment resource  [(xml)](design_usecases_CreateRARecord.html#25-new-list-resource---xml-example) [(json)](design_usecases_CreateRARecord.html#26-new-list-resource---json-example)
    * ClientSystem submits Create List request [(xml)](design_usecases_CreateRARecord.html#39-create-list-request---xml-example) [(json)](design_usecases_CreateRARecord.html#310-create-list-request---json-example)
      * ServerSystem submits Create List response [(xml)](design_usecases_CreateRARecord.html#311-create-list-response---xml-example) [(json)](design_usecases_CreateRARecord.html#312-create-list-response---json-example)

---

## 2 New Resource Examples ##

Examples of client-side resources as they are created. i.e. befoer they are written to Spine.

### 2.1 New Consent Resource - xml example ###
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-NewConsentResource.xml"
title="New Consent Resource"
type="xml" %}
### 2.2 New Consent Resource - json example ###
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-NewConsentResource.json"
title="New Consent Resource"
type="json" %}
### 2.3 New Impairment Resource - xml example ###
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-NewImpairmentResource.xml"
title="New Impairment Resource"
type="xml" %}
### 2.4 New Impairment Resource - json example ###
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-NewImpairmentResource.json"
title="New Impairment Resource"
type="json" %}
### 2.5 New List Resource - xml example ###
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-NewListResource.xml"
title="New List Resource"
type="xml" %}
### 2.6 New List Resource - json example ###
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-NewListResource.json"
title="New List Resource"
type="json" %}

## 3 Interaction Examples ##

Examples of http requests, responses and payloads

### 3.1 Create Consent Request - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Consent HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConsentRequest.xml"
title="Create Consent Request"
type="xml" %}


### 3.2 Create Consent Request - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Consent HTTP/1.1
Authorization:Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConsentRequest.json"
title="Create Consent Request"
type="json" %}


### 3.3 Create Consent Response - xml example ###
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


### 3.4 Create Consent Response - json example ###
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


### 3.5 Create Condition Request - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Condition HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConditionRequest.xml"
title="Create Condition Request"
type="xml" %}


### 3.6 Create Condition Request - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Condition HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConditionRequest.json"
title="Create Condition Request"
type="json" %}


### 3.7 Create Condition Response - xml example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Condition/57f04652-6dd0-4135-a560-f9091b1b26fa/_history/557ccfc3-0c78-48bf-aedd-70cc08af2ba1
ETag: W/"557ccfc3-0c78-48bf-aedd-70cc08af2ba1”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConditionResponse.xml"
title="Create Condition Response"
type="xml" %}


### 3.8 Create Condition Response - json example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Condition/57f04652-6dd0-4135-a560-f9091b1b26fa/_history/557ccfc3-0c78-48bf-aedd-70cc08af2ba1
ETag: W/"557ccfc3-0c78-48bf-aedd-70cc08af2ba1”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateConditionResponse.json"
title="Create Condition Response"
type="json" %}


### 3.9 Create List Request - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/List HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateListRequest.xml"
title="Create List Request"
type="xml" %}


### 3.10 Create List Request - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/List HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateListRequest.json"
title="Create List Request"
type="json" %}


### 3.11 Create List Response - xml example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:01 GMT
Last-Modified:2018-07-23T11:00:01+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/List/e00c5a85-d34f-4075-96ac-b787deb484b1/_history/5b703b55-cedc-4c19-b2aa-0666384eab1a
ETag: W/"5b703b55-cedc-4c19-b2aa-0666384eab1a”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateListResponse.xml"
title="Create List Response"
type="xml" %}


### 3.12 Create List Response - json example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:01 GMT
Last-Modified:2018-07-23T11:00:01+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/List/e00c5a85-d34f-4075-96ac-b787deb484b1/_history/5b703b55-cedc-4c19-b2aa-0666384eab1a
ETag: W/"5b703b55-cedc-4c19-b2aa-0666384eab1a”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/CreateExample-CreateListResponse.json"
title="Create List Response"
type="json" %}


---
---
