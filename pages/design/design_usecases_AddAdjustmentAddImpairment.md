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
  * System retrieves and displays RARecord for Patient's NHS Number

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
    [(xml)](design_usecases_AddAdjustmentAddImpairment.html#21-create-condition-resource---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#22-create-condition-resource---json-example)
* Practitioner commits RARecord
  * ClientSystem submits Create Flag request [(xml)](design_usecases_AddAdjustmentAddImpairment.html#23-create-flag-request---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#24-create-flag-request---json-example)
    * ServerSystem submits Create Flag response [(xml)](design_usecases_AddAdjustmentAddImpairment.html#25-create-flag-response---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#26-create-flag-response---json-example)
    
  * ClientSystem captures and structures Provenance information as new Provenance (RARecord-Provenance-1) resource [(xml)](design_usecases_AddAdjustmentAddImpairment.html#27-create-provenance-resource---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#28create-provenance-resource---json-example)
    * ClientSystem contains new Impairment resource within CareConnect-RARecord-List-1 resource
    * ClientSystem contains new Provenance resource within CareConnect-RARecord-List-1 resource [(xml)](design_usecases_AddAdjustmentAddImpairment.html#29-add-to-list-condition-resource---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#210-add-to-list-condition-resource---json-example)
    * ClientSystem submits Update List Condition request [(xml)](design_usecases_AddAdjustmentAddImpairment.html#211-update-list-condition-request---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#212-update-list-condition-request---json-example)
      * ServerSystem submits Update List Condition response [(xml)](design_usecases_AddAdjustmentAddImpairment.html#213-update-list-condition-response---xml-example) [(json)](design_usecases_AddAdjustmentAddImpairment.html#214-update-list-condition-response---json-example)

## 2 Interaction Examples ##

Examples of resources, http requests, responses and payloads

### 2.1 Create Condition Resource - xml example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateConditionRequest.xml"
title="Create Condition Resource"
type="xml" %}

### 2.2 Create Condition Resource - json example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create Condition Resource"
type="json" %}


### 2.3 Create Flag Request - xml example ###

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

### 2.4 Create Flag Request - json example ###

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
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create Flag Request"
type="json" %}

### 2.5 Create Flag Response - xml example ###

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

### 2.6 Create Flag Response - json example ###

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
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create Flag Response"
type="json" %}


### 2.7 Create Provenance Resource - xml example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-CreateProvenanceResource.xml"
title="Create Provenance Resource"
type="xml" %}

### 2.8 Create Provenance Resource - json example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create Provenance Resource"
type="json" %}

### 2.9 Add to List Condition Resource - xml example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-ListConditionResource.xml"
title="Create List Condition Resource"
type="xml" %}

### 2.10 Add to List Condition Resource - json example ###
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create List Condition Resource"
type="json" %}


### 2.11 Update List Condition Request - xml example ###
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
relfilepath="usecaseexamples/AddExample-ListConditionResource.xml"
title="Create List Condition Request"
type="xml" %}


### 2.12 Update List Condition Request - json example ###
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
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create List Condition Request"
type="json" %}


### 2.13 Update List Condition Response - xml example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/List/130f416a-055d-4a5d-a453-2b7c2de3b57b/_history/9554c538-1661-43b1-921b-efcbd2991c90
ETag: W/"9554c538-1661-43b1-921b-efcbd2991c90”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AddExample-ListConditionResponse.xml"
title="Create List Condition Response"
type="xml" %}


### 2.14 Update List Condition Response - json example ###
#### http response & headers ####
```
HTTP/1.1 201 Created
Date: Tue, 23 Jul 2018 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/List/130f416a-055d-4a5d-a453-2b7c2de3b57b/_history/9554c538-1661-43b1-921b-efcbd2991c90
ETag: W/"9554c538-1661-43b1-921b-efcbd2991c90”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Create List Condition Response"
type="json" %}


---
---
