---
title: Use Case | Multiple Conditions Read
keywords: usecase
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_MultipleConditionsRead.html
summary: Description of use case on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Multiple Conditions Read ##

#### Pre ####
* Practitioner creates RARecord, recording Consent from Patient and that Impairment is ‘Learning Disability’.
* Patient declines to record a specific Adjustment at this time.
see [Create RARecord Use Case](/design_usecases_create.html#1-create-rarecord-use-case)
* Practitioner adds Impairment 'Mental Health Condition', supporting Information 'Patient diagnosed with Stranger anxiety (disorder). Consider home-visit.'

#### Main ####
* Patient arrives for appointment; Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve RARecord
    * _ClientSystem submits Read Consent request (for Patient, Active, etc.)_
      * _ServerSystem submits Read Consent response_
    * _ClientSystem submits Read Flag request (for Patient, Active, etc.)_
      * _ServerSystem submits Read Flag response_  
<br>
_[Read Consent and Read Flag not illustrated_ - these are identical to existing [Read RA Record Use Case](/design_usecases_ReadRARecord.html#2-interaction-examples)]  
<br>
    * ClientSystem submits Read List request (for Patient, Active, etc.) [(xml)](design_usecases_MultipleConditionsRead.html#21-read-list-request---xml-example) [(json)](design_usecases_MultipleConditionsRead.html#22-read-list-request---json-example)
      * ServerSystem submits Read List response [(xml)](design_usecases_MultipleConditionsRead.html#23-read-list-response---xml-example) [(json)](design_usecases_MultipleConditionsRead.html#24-read-list-response---json-example)
    * ClientSystem submits Read Conditions request [(xml)](design_usecases_MultipleConditionsRead.html#25-read-conditions-request---xml-example) [(json)](design_usecases_MultipleConditionsRead.html#26-read-conditions-request---json-example)
      * ServerSystem submits Read Conditions response [(xml)](design_usecases_MultipleConditionsRead.html#27-read-conditions-response---xml-example) [(json)](design_usecases_MultipleConditionsRead.html#28-read-conditions-response---json-example)

### 2.1 Read List request - xml example  ###

#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
 patient=999999998&
 status=current&
 code=http://snomed.info/sct|1094391000000102&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.read:1

```

#### http body ####
**None**

### 2.2 Read List request - json example  ###

#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
 patient=999999998&
 status=current&
 code=http://snomed.info/sct|1094391000000102&
 _format=json HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.read:1

```

#### http body ####
**None**

### 2.3 Read List response - xml example  ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 12:00:00 GMT
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/SearchSetListBundleResponse.xml"
title="Read List response bundle"
type="xml" %}

### 2.4 Read List response - json example  ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 12:00:00 GMT
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/SearchSetListBundleResponse.json"
title="Read List response bundle"
type="json" %}

### 2.5 Read Conditions request - xml example  ###

#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Condition?
 _list=e00c5a85-d34f-4075-96ac-b787deb484b1&
 clinical-status=active&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.read:1

```

Idiomatically this is 'Get all Conditions on List e00c5a85-d34f-4075-96ac-b787deb484b1, whose clinicalStatus is active'.  
**NB.**Spelling of search parameter 'clinical-status' versus element Condition.clinicalStatus  

#### http body ####
**None**

### 2.6 Read Conditions request - json example  ###

#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Condition?
 _list=e00c5a85-d34f-4075-96ac-b787deb484b1&
 clinical-status=active&
 _format=json HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Condition.read:1

```

Idiomatically this is 'Get all Conditions on List e00c5a85-d34f-4075-96ac-b787deb484b1, whose clinicalStatus is active'.  
**NB.**Spelling of search parameter 'clinical-status' versus element Condition.clinicalStatus  

#### http body ####
**None**

### 2.7 Read Conditions response - xml example  ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 12:00:01 GMT
Content-Type: application/fhir+xml

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/SearchSetConditionBundleResponse.xml"
title="Read Conditions response bundle"
type="xml" %}

### 2.8 Read Conditions response - json example  ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date: Tue, 24 Jul 2018 12:00:01 GMT
Content-Type: application/fhir+json

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/SearchSetConditionBundleResponse.json"
title="Read Conditions response bundle"
type="json" %}

---
---
