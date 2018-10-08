---
title: Use Case | Remove RA Record
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_RemoveRARecord.html
summary: Description of Removal of enire Reasonable Adjustments Record from Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Remove RA Record ##

#### Trigger ####
Practitioner wishes to remove an entire Reasonable Adjustment record

#### Summary ####
Practitioner enters Removal Reason. System inactivates all Reasonable Adjustment resources for Patient.  

#### Pre ####
* Practitioner has retrieved Patient's RA Flag. 

#### Trigger ####
* Practitioner selects Remove Reasonable Adjustments Flag
* or Practitioner removes Consent

#### Main ####
* Practitioner enters Removal Reason
  * ClientSystem generates new Parameter resource [(xml)](design_usecases_RemoveRARecord.html#21-parameter-resource---xml-example) [(json)](design_usecases_RemoveRARecord.html#22-parameter-resource---json-example)
  * ClientSystem submits Remove RA Record [(xml)](design_usecases_RemoveRARecord.html#31-removerarecord-operation---xml-example) [(json)](design_usecases_RemoveRARecord.html#31-removerarecord-operation---json-example)
    * ServerSystem submits Remove RA Record response[(xml)](design_usecases_RemoveRARecord.html#33-removerarecord-operation-outcome---xml-example) [(json)](design_usecases_RemoveRARecord.html#34-removerarecord-operation-outcome---json-example)

## 2 New Example ##

Examples of client-side resources.

### 2.1 Parameter Resource - xml example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveRARecord-ParameterResource.xml"
title="Updated Flag Resource"
type="xml" %}

### 2.2 Parameter Resource - json example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveRARecord-ParameterResource.json"
title="Updated Flag Resource"
type="json" %}


## 3 Interaction Examples ##

### 3.1 Remove RA Record - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/$removerarecord HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:removerarecord.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveRARecord-OperationRequest.xml"
title="RemoveRARecord Operation Request"
type="xml" %}

### 3.2 Remove RA Record - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/$removerarecord HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:removerarecord.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveRARecord-OperationRequest.json"
title="RemoveRARecord Operation Request"
type="json" %}

### 3.3 Remove RA Record outcome - xml example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 25 Jul 2018 11:00:00 GMT
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveRARecord-OperationOutcome.xml"
title="RemoveRARecord Operation Outcome"
type="xml" %}

### 3.4 Remove RA Record outcome - json example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 25 Jul 2018 11:00:00 GMT
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveRARecord-OperationOutcome.json"
title="RemoveRARecord Operation Outcome"
type="json" %}