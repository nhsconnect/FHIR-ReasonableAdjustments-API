---
title: Use Case | Add Adjustment, Add Impairment
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_AddAdjustmentAddImpairment.html
summary: Description of use case on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Add Adjustment, Add Impairment ##

####  Trigger: ####
Pre-operative appointment with Learning Disability Nurse N.

####  System Scope: ####
ClientSystem includes GPSystem client, SCRa, 1-click etc.  
ServerSystem includes Spine, PDS, SDS, FlagServer etc.  

####  Summary: ####
During appointment Nurse discusses RA Record, Patient requests recording of 'Easy Read' Adjustment, addition of 'Mental Health Disability w supporting text' Impairment.

#### Pre ####

* Practitioner logged into ClientSystem, traces & verifies demographic info
* Practitioner opens Patient's RARecord
  * System retrieves and displays RARecord for Patient's NHS

* Practitioner discusses RARecord and RA with Patient
* Patient agrees to add Adjustment 'Easy Read'
* Patient agrees to add Impairment 'Mental Health Disability w supporting text'


#### Main ####

* Patient agrees to add Adjustment 'Easy Read'
  * Practitioner adds Adjustment from coded picklist
    * ClientSystem captures and structures as new RARecord-Flag-1 resource
* Patient agrees to add Impairment 'Mental Health Disability' with supporting text
  * Practitioner adds Impairment from coded picklist (elaborates w separate freetext)  
    * ClientSystem captures and structures Impairment information as new Impairment (CareConnect-RARecord-Condition-1) resource
* Practitioner commits RARecord
  * ClientSystem submits Create Flag request [(xml)](design_usecases_AddAdjustmentAddImpairment.html#21-create-flag-request---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#22-create-flag-request---json-example)
    * ServerSystem submits Create Flag response [(xml)](design_usecases_AddAdjustmentAddImpairment.html#23-create-flag-response---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#24-create-flag-response---json-example)
  * ClientSystem submits Create Condition request [(xml)](design_usecases_AddAdjustmentAddImpairment.html#25-create-condition-request---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#26-create-condition-request---json-example)
    * ServerSystem submits Create Condition response [(xml)](design_usecases_AddAdjustmentAddImpairment.html#27-create-condition-response---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#28-create-condition-response---json-example)
  * ClientSystem updates existing CareConnect-RARecord-List-1 to reference / identify new Impairment resource
  * ClientSystem submits Update List request [(xml)](design_usecases_AddAdjustmentAddImpairment.html#29-update-list-request---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#210-update-list-request---json-example)
    * ServerSystem submits Update List response [(xml)](design_usecases_AddAdjustmentAddImpairment.html#211-update-list-response---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#212-update-list-response---json-example)

## 2 Interaction Examples ##

Examples of http requests, responses and payloads

### 2.1 Create Flag Request - xml example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateFlagRequest.xml"
title="Create Flag Request"
type="xml" %}

### 2.2 Create Flag Request - json example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateFlagRequest.json"
title="Create Flag Request"
type="json" %}

### 2.3 Create Flag Response - xml example ###

#### http request & headers ####
```
HTTP/1.1 201 Created
Date: Wed, 24 Jul 2018 10:01:00 GMT
Last-Modified:2018-07-24T10:01:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Flag/2acb0536-0a8f-48c9-8a2f-6ee82860f186/_history/aa755bd6-2be9-4971-972a-6724879c5cb1
ETag: W/"aa755bd6-2be9-4971-972a-6724879c5cb1”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateFlagResponse.xml"
title="Create Flag Response"
type="xml" %}

### 2.4 Create Flag Response - json example ###

#### http request & headers ####
```
HTTP/1.1 201 Created
Date: Wed, 24 Jul 2018 10:01:00 GMT
Last-Modified:2018-07-24T10:01:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Flag/2acb0536-0a8f-48c9-8a2f-6ee82860f186/_history/aa755bd6-2be9-4971-972a-6724879c5cb1
ETag: W/"aa755bd6-2be9-4971-972a-6724879c5cb1”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateFlagResponse.json"
title="Create Flag Response"
type="json" %}

### 2.5 Create Condition Request - xml example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Condition HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateConditionRequest.xml"
title="Create Condition Request"
type="xml" %}

### 2.6 Create Condition Request - json example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Condition HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateConditionRequest.json"
title="Create Condition Request"
type="json" %}

### 2.7 Create Condition Response - xml example ###

#### http request & headers ####
```
HTTP/1.1 201 Created
Date: Wed, 24 Jul 2018 10:01:00 GMT
Last-Modified: 2018-07-24T10:01:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Condition/6be8bee9-e727-4564-a904-49507576f8be/_history/a9b91e41-30ad-43a4-a2da-79b9be622169
ETag: W/"a9b91e41-30ad-43a4-a2da-79b9be622169”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateConditionResponse.xml"
title="Create Condition Response"
type="xml" %}

### 2.8 Create Condition Response - json example ###

#### http request & headers ####
```
HTTP/1.1 201 Created
Date: Wed, 24 Jul 2018 10:01:00 GMT
Last-Modified: 2018-07-24T10:01:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Condition/6be8bee9-e727-4564-a904-49507576f8be/_history/a9b91e41-30ad-43a4-a2da-79b9be622169
ETag: W/"a9b91e41-30ad-43a4-a2da-79b9be622169”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateConditionResponse.json"
title="Create Condition Response"
type="json" %}

### 2.9 Update List Request - xml example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/e00c5a85-d34f-4075-96ac-b787deb484b1 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"5b703b55-cedc-4c19-b2aa-0666384eab1a"


```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-UpdateListRequest.xml"
title="Update List Request"
type="xml" %}

### 2.10 Update List Request - json example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/e00c5a85-d34f-4075-96ac-b787deb484b1 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"5b703b55-cedc-4c19-b2aa-0666384eab1a"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-UpdateListRequest.json"
title="Update List Request"
type="json" %}

### 2.11 Update List Response - xml example ###

#### http request & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 10:02:00 GMT
Last-Modified:2018-07-24T10:02:00+00:00
ETag: W/"a8cbe427-7195-482e-81ff-b5809db6d08c”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-UpdateListResponse.xml"
title="Update List Response"
type="xml" %}

### 2.12 Update List Response - json example ###

#### http request & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 10:02:00 GMT
Last-Modified:2018-07-24T10:02:00+00:00
ETag: W/"a8cbe427-7195-482e-81ff-b5809db6d08c”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-UpdateListResponse.json"
title="Update List Response"
type="json" %}

---
---
