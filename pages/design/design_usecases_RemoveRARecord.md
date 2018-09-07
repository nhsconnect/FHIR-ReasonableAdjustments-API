---
title: Use Case | Remove RA Record
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_RemoveRARecord.html
summary: Description of use case on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Remove RA Record ##

#### Trigger ####
Practitioner wishes to remove an entire Reasonable Adjustment record

#### Summary ####
Practitioner enters Removal Reason. System inactivates all Reasonable Adjustment resources for Patient.  

#### Pre ####
* Practitionwer has retrieved Patient's RA Flag. 

#### Main ####
* Practitioner enters Removal Reason
  * ClientSystem generates new Parameter resource [(xml)](design_usecases_RemoveRARecord.html#21-parameter-resource---xml-example) [(json)](design_usecases_RemoveRARecord.html#22-parameter-resource---json-example)
  * ClientSystem submits removeflag operation [(xml)](design_usecases_RemoveRARecord.html#31-removeflag-operation---xml-example) [(json)](design_usecases_RemoveRARecord.html#31-removeflag-operation---json-example)
    * ServerSystem submits removeflag operation response[(xml)](design_usecases_RemoveRARecord.html#33-removeflag-operation-outcome---xml-example) [(json)](design_usecases_RemoveRARecord.html#34-removeflag-operation-outcome---json-example)

## 2 New Example ##

Examples of client-side resources.

### 2.1 Parameter Resource - xml example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveFlag-ParameterResource.xml"
title="Updated Flag Resource"
type="xml" %}

### 2.2 Parameter Resource - json example ###

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveFlag-ParameterResource.json"
title="Updated Flag Resource"
type="json" %}


## 3 Interaction Examples ##

### 3.1 removeflag operation - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/$removeflag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:removeflag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveFlag-OperationRequest.xml"
title="RemoveFlag Operation Request"
type="xml" %}

### 3.2 removeflag operation - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/$removeflag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Content-Type: application/fhir+json
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:removeflag.write:1

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveFlag-OperationRequest.json"
title="RemoveFlag Operation Request"
type="json" %}

### 3.3 removeflag operation outcome - xml example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 25 Jul 2018 11:00:00 GMT
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveFlag-OperationOutcome.xml"
title="RemoveFlag Operation Outcome"
type="xml" %}

### 3.4 removeflag operation outcome - json example ###
#### http request & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 25 Jul 2018 11:00:00 GMT
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RemoveFlag-OperationOutcome.json"
title="RemoveFlag Operation Outcome"
type="json" %}