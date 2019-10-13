---
title: Use Case | Remove Impairment
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_RemoveImpairment.html
summary: Description of use case on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Remove Impairment ##

Although unlikely, Update Contention is possible. This scenario illustrates the case where Practitioners A and B try to remove a resource 'at the same time'. 'Optimistic locking' is used, so A, who writes first 'wins'.
#### Pre ####
* Practitioner A reads Patient's RARecord
* Practitioner B reads Patient's RARecord

* Practitioner A updates Patient's RARecord, Remove an Impairment 'Mental Health Condition' operation
  * Practitioner A commits update
    * ClientSystem captures and structures Provenance information as new Provenance (RARecord-Provenance-1) resource
    * ClientSystem contains new Provenance resource within CareConnect-RARecord-List-1 resource
    * ClientSystem marks Impairment List.entry element in CareConnect-RARecord-List-1 resource as deleted [(xml)](design_usecases_RemoveImpairment.html#21-delete-condition-a-resource---xml-example) [(json)](design_usecases_RemoveImpairment.html#22-delete-condition-a-resource---json-example)
    * ClientSystem submits Update List (A)request [(xml)](design_usecases_RemoveImpairment.html#23-update-list-request---xml-example) [(json)](design_usecases_RemoveImpairment.html#24-update-list-request---json-example)
      * ServerSystem submits Update List response [(xml)](design_usecases_RemoveImpairment.html#25-update-list-response---xml-example) [(json)](design_usecases_RemoveImpairment.html#26-update-list-response---json-example)
* Practitioner B updates Patient's RARecord, Remove an Impairment 'Mental Health Condition' operation
  * Practitioner B commits update
    * ClientSystem submits Update List (B) request [(xml)](design_usecases_RemoveImpairment.html#27-update-list-b-request---xml-example) [(json)](design_usecases_RemoveImpairment.html#28-update-list-b-request---json-example)
      * ServerSystem submits Update List (B) response (failure) [(xml)](design_usecases_RemoveImpairment.html#29-update-list-b-response---xml-example) [(json)](design_usecases_RemoveImpairment.html#210-update-list-b-response---json-example)
    * ClientSystem reports failure, aborts.

## 2 Interaction Examples ##

### 2.1 Delete Condition A Resource - xml example
#### resource ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteExample-RemoveConditionListResource.xml"
title="Delete Condition List Resource A"
type="xml" %}

### 2.2 Delete Condition A Resource - json example
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Delete Condition List Resource A"
type="json" %}

### 2.3 Update List Request - xml example
#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/130f416a-055d-4a5d-a453-2b7c2de3b57b HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"9554c538-1661-43b1-921b-efcbd2991c90"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteExample-RemoveConditionListResource.xml"
title="Update List Request example"
type="xml" %}

### 2.4 Update List Request - json example
#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/130f416a-055d-4a5d-a453-2b7c2de3b57b HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"9554c538-1661-43b1-921b-efcbd2991c90"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Update List Request example"
type="json" %}


### 2.5 Update List Response - xml example
#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 25 Jul 2018 11:00:03 GMT
Last-Modified:2018-07-25T11:00:02+00:00
ETag: W/"d65be6d8-128a-40f2-9a1d-b250d6485c6d”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionInstance2Response.xml"
title="Update List Response"
type="xml" %}


### 2.6 Update List Response - json example
#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 25 Jul 2018 11:00:03 GMT
Last-Modified:2018-07-25T11:00:02+00:00
ETag: W/"d65be6d8-128a-40f2-9a1d-b250d6485c6d”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Update List Response"
type="json" %}


### 2.7 Update List B Request - xml example
#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/130f416a-055d-4a5d-a453-2b7c2de3b57b HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"9554c538-1661-43b1-921b-efcbd2991c90"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteExample-RemoveConditionListResourceB.xml"
title="Update List B Request example"
type="xml" %}


### 2.8 Update List B Request - json example
#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/130f416a-055d-4a5d-a453-2b7c2de3b57b HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"9554c538-1661-43b1-921b-efcbd2991c90"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/AAJSONPlaceholder.json"
title="Update List B Request example"
type="json" %}


### 2.9 Update List B Response - xml example
#### http response & headers ####
```
HTTP/1.1 409 CONFLICT
Date: Tue, 25 Jul 2018 11:02:03 GMT
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionFailOperationOutcome.xml"
title="Read Fail Operation Outcome"
type="xml" %}

### 2.10 Update List B Response - json example
#### http response & headers ####
```
HTTP/1.1 409 CONFLICT
Date: Tue, 25 Jul 2018 11:02:03 GMT
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionFailOperationOutcome.json"
title="Read Fail Operation Outcome"
type="json" %}

---
---