---
title: Interaction | Update
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_update_remix.html
summary: Update operation describes interaction required to update a Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Add Adjustment; Add Impairment ##

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
    * ClientSystem captures and structures as new RARecord-Flag-1 resource [(xml)](design_usecases_update_remix.html#21-new-adjustment-resource---xml-example) [(json)](design_usecases_update_remix.html#22-new-adjustment-resource---json-example)

* Patient agrees to add Impairment 'Mental Health Disability' with supporting text
  * Practitioner adds Impairment from coded picklist (elaborates w separate freetext)  
    * ClientSystem captures and structures Impairment information as new Impairment (CareConnect-RARecord-Condition-1) resource [(xml)](design_usecases_update_remix.html#23-new-impairment-resource---xml-example) [(json)](design_usecases_update_remix.html#24-new-impairment-resource---json-example)

* Practitioner commits RARecord
  * ClientSystem submits Create Flag request [(xml)](design_usecases_update_remix.html#31-create-flag-request---xml-example) [(json)](design_usecases_update_remix.html#32-create-flag-request---json-example)
    * ServerSystem submits Create Flag response [(xml)](design_usecases_update_remix.html#33-create-flag-response---xml-example) [(json)](design_usecases_update_remix.html#34-create-flag-response---json-example)
  * ClientSystem submits Create Condition request [(xml)](design_usecases_update_remix.html#35-create-condition-request---xml-example) [(json)](design_usecases_update_remix.html#36-create-condition-request---json-example)
    * ServerSystem submits Create Condition response [(xml)](design_usecases_update_remix.html#37-create-condition-response---xml-example) [(json)](design_usecases_update_remix.html#38-create-condition-response---json-example)
  * ClientSystem updates existing CareConnect-RARecord-List-1 to reference / identify new Impairment resource [(xml)](design_usecases_update_remix.html#25-updated-list-resource---xml-example) [(json)](design_usecases_update_remix.html#26-updated-list-resource---json-example)
  * ClientSystem submits Update List request [(xml)](design_usecases_update_remix.html#39-update-list-request---xml-example) [(json)](design_usecases_update_remix.html#310-update-list-request---json-example)
    * ServerSystem submits Update List response [(xml)](design_usecases_update_remix.html#311-update-list-response---xml-example) [(json)](design_usecases_update_remix.html#312-update-list-response---json-example)


## 2 New Resource Examples ##

Examples of client-side resources as they are created. i.e. before they are written to Spine.

### 2.1 New Adjustment Resource - xml example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-NewAdjustmentResource.xml"
title="New Adjustment Resource"
type="xml" %}

### 2.2 New Adjustment Resource - json example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-NewAdjustmentResource.json"
title="New Adjustment Resource"
type="json" %}

### 2.3 New Impairment Resource - xml example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-NewImpairmentResource.xml"
title="New Impairment Resource"
type="xml" %}

### 2.4 New Impairment Resource - json example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-NewImpairmentResource.json"
title="New Impairment Resource"
type="json" %}

### 2.5 Updated List Resource - xml example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-UpdatedListResource.xml"
title="Updated List Resource"
type="xml" %}

### 2.6 Updated List Resource - json example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-UpdatedListResource.json"
title="Updated List Resource"
type="json" %}

## 3 Interaction Examples ##

Examples of http requests, responses and payloads

### 3.1 Create Flag Request - xml example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateFlagRequest.xml"
title="Create Flag Request"
type="xml" %}

### 3.2 Create Flag Request - json example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateFlagRequest.json"
title="Create Flag Request"
type="json" %}

### 3.3 Create Flag Response - xml example ###

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

### 3.4 Create Flag Response - json example ###

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

### 3.5 Create Condition Request - xml example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Condition HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateConditionRequest.xml"
title="Create Condition Request"
type="xml" %}

### 3.6 Create Condition Request - json example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Condition HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateConditionRequest.json"
title="Create Condition Request"
type="json" %}

### 3.7 Create Condition Response - xml example ###

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

### 3.8 Create Condition Response - json example ###

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

### 3.9 Update List Request - xml example ###

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

### 3.10 Update List Request - json example ###

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

### 3.11 Update List Response - xml example ###

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

### 3.12 Update List Response - json example ###

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

## 4 Update Adjustment ##

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

* Practitioner removes (soft deletes) existing 'Easy Read' Adjustment, records Removal reason 'Entered in error';
  * ClientSystem updates client-side Flag resource [(xml)](design_usecases_update_remix.html#51-updated-flag-resource---xml-example) [(json)](design_usecases_update_remix.html#52-updated-flag-resource---json-example)

* Practitioner commits RARecord
  * ClientSystem submits Update Flag request [(xml)](design_usecases_update_remix.html#61-update-flag-request---xml-example) [(json)](design_usecases_update_remix.html#62-update-flag-request---json-example)
    * ServerSystem submits Update Flag response [(xml)](design_usecases_update_remix.html#63-update-flag-response---xml-example) [(json)](design_usecases_update_remix.html#64-update-flag-response---json-example)

* Practitioner records new 'Large Print' Adjustment
  * ClientSystem captures and structures Adjustment information as new RARecord-Flag-1 resource [(xml)](design_usecases_update_remix.html#53-new-flag-resource---xml-example) [(json)](design_usecases_update_remix.html#54-new-flag-resource---json-example)

* Practitioner commits RARecord
  * ClientSystem submits Create Flag request [(xml)](design_usecases_update_remix.html#65-create-flag-request---xml-example) [(json)](design_usecases_update_remix.html#66-create-flag-request---json-example)
    * ServerSystem submits Create Flag response [(xml)](design_usecases_update_remix.html#67-create-flag-response---xml-example) [(json)](design_usecases_update_remix.html#68-create-flag-response---json-example)


## 5 New and Updated Resource Examples ##

Examples of client-side resources.

### 5.1 Updated Flag Resource - xml example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-UpdatedFlagResource.xml"
title="Updated Flag Resource"
type="xml" %}

### 5.2 Updated Flag Resource - json example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-UpdatedFlagResource.json"
title="Updated Flag Resource"
type="json" %}

### 5.3 New Flag Resource - xml example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-NewFlagResource.xml"
title="New Flag Resource"
type="xml" %}

### 5.4 New Flag Resource - json example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-NewFlagResource.json"
title="New Flag Resource"
type="json" %}

## 6 Interaction Examples ##

Examples of http requests, responses and payloads

### 6.1 Update Flag Request - xml example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Flag/2acb0536-0a8f-48c9-8a2f-6ee82860f186 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1
If-Match: W/"aa755bd6-2be9-4971-972a-6724879c5cb1"


```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-UpdateFlagRequest.xml"
title="UpdateFlagRequest.xml"
type="xml" %}

### 6.2 Update Flag Request - json example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Flag/2acb0536-0a8f-48c9-8a2f-6ee82860f186 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1
If-Match: W/"aa755bd6-2be9-4971-972a-6724879c5cb1"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-UpdateFlagRequest.json"
title="Update Flag Request"
type="json" %}

### 6.3 Update Flag Response - xml example ###

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

### 6.4 Update Flag Response - json example ###

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

### 6.5 Create Flag Request - xml example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-CreateFlagRequest.xml"
title="Create Flag Request"
type="xml" %}

### 6.6 Create Flag Request - json example ###

#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/UpdateExample-CreateFlagRequest.json"
title="Create Flag Request"
type="json" %}

### 6.7 Create Flag Response - xml example ###

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

### 6.8 Create Flag Response - json example ###

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

