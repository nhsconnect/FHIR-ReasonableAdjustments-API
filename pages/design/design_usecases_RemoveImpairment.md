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

#### Main ####
* Practitioner A updates Patient's RARecord, Remove an Impairment 'Mental Health Condition' operation
  * Practitioner A commits update
    * ClientSystem submits Delete Condition (A) request [(xml)](design_usecases_RemoveImpairment.html#21-delete-condition-a-request---xml-example) [(json)](design_usecases_RemoveImpairment.html#22-delete-condition-a-request---json-example)
      * ServerSystem submits Delete Condition (A) response [(xml)](design_usecases_RemoveImpairment.html#23-delete-condition-a-response---xml-example) [(json)](design_usecases_RemoveImpairment.html#24-delete-condition-a-response---json-example)
    * ClientSystem submits Update List request [(xml)](design_usecases_RemoveImpairment.html#25-update-list-request---xml-example) [(json)](design_usecases_RemoveImpairment.html#26-update-list-request---json-example)
      * ServerSystem submits Update List response [(xml)](design_usecases_RemoveImpairment.html#27-update-list-response---xml-example) [(json)](design_usecases_RemoveImpairment.html#28-update-list-response---json-example)
* Practitioner B updates Patient's RARecord, Remove an Impairment 'Mental Health Condition' operation
  * Practitioner B commits update
    * ClientSystem submits Delete Condition (B) request [(xml)](design_usecases_RemoveImpairment.html#29-delete-condition-b-request---xml-example) [(json)](design_usecases_RemoveImpairment.html#210-delete-condition-b-request---json-example)
      * ServerSystem submits Delete Condition (B) response (failure) [(xml)](design_usecases_RemoveImpairment.html#211-delete-condition-b-response---xml-example) [(json)](design_usecases_RemoveImpairment.html#212-delete-condition-b-response---json-example)
    * ClientSystem reports failure, aborts.

## 2 Interaction Examples ##

### 2.1 Delete Condition (A) request - xml example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Condition/13aec731-02c5-42a2-b863-de889479e777 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1
If-Match: W/"cf8e1249-dfa6-4003-9745-d1b213008c95"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionInstance2Request.xml"
title="Delete Condition request example"
type="xml" %}


### 2.2 Delete Condition (A) request - json example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Condition/13aec731-02c5-42a2-b863-de889479e777 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1
If-Match: W/"cf8e1249-dfa6-4003-9745-d1b213008c95"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionInstance2Request.json"
title="Delete Condition request example"
type="json" %}


### 2.3 Delete Condition (A) response - xml example ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 10:00:01 GMT
Last-Modified:2018-07-24T10:00:02+00:00
ETag: W/"0bf0b49c-9dfb-4587-9931-0b4a00819229”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionInstance2Response.xml"
title="Delete Condition request example"
type="xml" %}

### 2.4 Delete Condition (A) response - json example ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 10:00:01 GMT
Last-Modified:2018-07-24T10:00:02+00:00
ETag: W/"0bf0b49c-9dfb-4587-9931-0b4a00819229”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionInstance2Response.json"
title="Delete Condition request example"
type="json" %}

### 2.5 Update List request - xml example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/4c8d19af-7755-4954-93df-93c964ddf349 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"bb325b55-e8a0-41df-84bd-3ac2b026ab5b"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/ListInstanceUpdateRequest.xml"
title="Update List request example"
type="xml" %}

### 2.6 Update List request - json example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/4c8d19af-7755-4954-93df-93c964ddf349 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"bb325b55-e8a0-41df-84bd-3ac2b026ab5b"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/ListInstanceUpdateRequest.json"
title="Update List request example"
type="json" %}

### 2.7 Update List response - xml example ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 10:00:02 GMT
Last-Modified:2018-07-24T10:00:02+00:00
ETag: W/"3de1a085-95f3-43d2-be3c-aa60b6b3da85”
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/ListInstanceUpdateResponse.xml"
title="Update List response example"
type="xml" %}

### 2.8 Update List response - json example ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 10:00:02 GMT
Last-Modified:2018-07-24T10:00:02+00:00
ETag: W/"3de1a085-95f3-43d2-be3c-aa60b6b3da85”
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/ListInstanceUpdateResponse.json"
title="Update List response example"
type="json" %}

### 2.9 Delete Condition (B) request - xml example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Condition/13aec731-02c5-42a2-b863-de889479e777 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1
If-Match: W/"cf8e1249-dfa6-4003-9745-d1b213008c95"

```
The only material difference between this request and Delete Condition (A) request will be time/order of receipt, and in the JWT payload.  

#### http body ####
[As example above](/design_usecases_RemoveImpairment.html#21-delete-condition-a-request---xml-example)

### 2.10 Delete Condition (B) request - json example ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Condition/13aec731-02c5-42a2-b863-de889479e777 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.write:1
If-Match: W/"cf8e1249-dfa6-4003-9745-d1b213008c95"

```
The only material difference between this request and Delete Condition (A) request will be time/order of receipt, and in the JWT payload.  

#### http body ####
[As example above](/design_usecases_RemoveImpairment.html#22-delete-condition-a-request---json-example)

### 2.11 Delete Condition (B) response - xml example ###

#### http response & headers ####
```
HTTP/1.1 409 CONFLICT
Date: Tue, 24 Jul 2018 10:10:02 GMT
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionFailOperationOutcome.xml"
title="Read Fail Operation Outcome"
type="xml" %}

### 2.12 Delete Condition (B) response - json example ###

#### http response & headers ####
```
HTTP/1.1 409 CONFLICT
Date: Tue, 24 Jul 2018 10:10:02 GMT
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionFailOperationOutcome.json"
title="Read Fail Operation Outcome"
type="json" %}

---
---