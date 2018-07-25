---
title: Interaction | Use Case Examples Remix
keywords: usecase
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_remix.html
summary: Updated Use Cases and examples illustrating requirements for operation of the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

Use Case Remix
==============


## 1 Initial Read Failure - No RA Record ##

#### Pre ####
* None

#### Main ####
* Practitioner searches for Patient's RARecord
  * ClientSystem searched and failed to find existing RARecord
    * ClientSystem submits [Read Consent request](/design_usecases_remix.html#11-read-consent-request) (for Patient, Active, etc.)
    * ServerSystem submits [Read Consent response](/design_usecases_remix.html#12-read-consent-response)

### 1.1 Read Consent request - xml example  ###

#### http request & headers ####

```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver

```
### 1.2 Read Consent request - json example  ###

#### http request & headers ####

```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=json HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver

```

#### http body ####
**None**

### 1.3 Read Consent response - xml example ###

#### http response & headers ####
```
HTTP/1.1 404 NOT FOUND
Date:Tue, 24 Jul 2018 10:00:00 GMT
Content-Type:application/xml+fhir

```
**DQ:** Would you use full header & metadata in a failure OperationOutcome response?  
**DN:** Can't see why you would.  
From FHIR spec, 'The resource is not designed to be persisted or referenced from other parts of the workflow.'  
Therefore it won't have a versionId/ETag, lastModified would only ever be the same as Date, no Location as not persisted.
Failure response therefore drops to minimal Date, Content-Type headers.
#### http body ####
```
<!-- Spine-operationOutcome-1 instance -->
<OperationOutcome xmlns="http://hl7.org/fhir">
    <id value="44d3b0d1-013e-43bd-ad99-994e8cbae769"/>
    <meta>
        <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"/>
    </meta>
    <issue>
        <severity value="error"/>
        <code value="not-found"/>
        <details>
            <coding>
                <system value="https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1"/>
                <code value="NO_RECORD_FOUND"/>
                <display value="No record found"/>
            </coding>
        </details>
    </issue>
</OperationOutcome>
```
### 1.4 Read Consent response - json example ###

#### http response & headers ####
```
HTTP/1.1 404 PATIENT NOT FOUND
Date:Tue, 24 Jul 2018 10:00:00 GMT
Content-Type:application/json+fhir

```

#### http body ####
```
{ "OperationOutcome" : 

}

```

## 2 Multiple Conditions Read (one with freetext) ##

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
_[Read Consdent and Read Flag not illustrated_ - these are identical to existing [Read RA Record Use Case](/design_usecases_read.html#2-read-ra-record-use-case-examples)]  
<br>
    * ClientSystem submits [Read List request](/design_usecases_remix.html#21-read-list-request) (for Patient, Active, etc.)
      * ServerSystem submits [Read List response](/design_usecases_remix.html#22-read-list-response)
    * ClientSystem submits [Read Conditions request](/design_usecases_remix.html#23-read-conditions-request)
      * ServerSystem submits [Read Conditions response](/design_usecases_remix.html#24-read-conditions-response)

### 2.1 Read List request ###

#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
 patient=999999998&
 status=current&
 code=http://snomed.info/sct|1094391000000102&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver

```

#### http body ####
**None**

### 2.2 Read List response ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 10:00:00 GMT
Last-Modified:2018-07-24T10:00:00+00:00
ETag: W/"9b8509a6-2330-448c-aefc-1d6f723f3e5e”
Content-Type:application/xml+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/SearchSetListBundleResponse.xml"
title="Read List response bundle"
type="xml" %}

### 2.3 Read Conditions request ###

#### http request & headers ####
```
GET https://clinicals.spineservices.nhs.uk/STU3/Condition?
 _list=4c8d19af-7755-4954-93df-93c964ddf349&
 clinical-status=active&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver

```

Idiomatically this is 'Get all Conditions on List 4c8d19af-7755-4954-93df-93c964ddf349, whose clinicalStatus is active'.  
**NB.**Spelling of search parameter 'clinical-status' versus element Condition.clinicalStatus  

#### http body ####
**None**

### 2.4 Read Conditions response ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 10:00:01 GMT
Last-Modified:2018-07-24T10:00:01+00:00
ETag: W/"ded2da33-64c9-4c8d-8e3a-6a037823d0c6”
Content-Type:application/xml+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/SearchSetConditionBundleResponse.xml"
title="Read Conditions response bundle"
type="xml" %}

## 3 Update Contention failure ##

Although unlikely, Update Contention is possible. This scenario illustrates the case where Practitioners A and B try to update a resource 'at the same time'. 'Optimistic locking' is used, so A, who writes first 'wins'.
#### Pre ####
* Practitioner A reads Patient's RARecord
* Practitioner B reads Patient's RARecord

#### Main ####
* Practitioner A updates Patient's RARecord, Remove an Impairment 'Mental Health Condition' operation
  * Practitioner A commits update
    * ClientSystem submits Delete Condition (A) request
      * ServerSystem submits Delete Condition (A) response
    * ClientSystem submits Update List request
      * ServerSystem submits Update List response
* Practitioner B updates Patient's RARecord, Remove an Impairment 'Mental Health Condition' operation
  * Practitioner B commits update
    * ClientSystem submits Delete Condition (B) request
      * ServerSystem submits Delete Condition (B) response (failure)
    * ClientSystem reports failure, aborts.

### 3.1 Delete Condition (A) request ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Condition/13aec731-02c5-42a2-b863-de889479e777
 Authorization:Bearer [jwt_token_string]
 InteractionID:urn:nhs:names:services:flagserver
 If-Match:W/"cf8e1249-dfa6-4003-9745-d1b213008c95"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionInstance2Request.xml"
title="Delete Condition request example"
type="xml" %}


### 3.2 Delete Condition (A) response ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 10:00:01 GMT
Last-Modified:2018-07-24T10:00:01+00:00
ETag: W/"0bf0b49c-9dfb-4587-9931-0b4a00819229”
Content-Type:application/xml+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/DeleteConditionInstance2Response.xml"
title="Delete Condition request example"
type="xml" %}

### 3.3 Update List request ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/4c8d19af-7755-4954-93df-93c964ddf349
 Authorization:Bearer [jwt_token_string]
 InteractionID:urn:nhs:names:services:flagserver
 If-Match:W/"bb325b55-e8a0-41df-84bd-3ac2b026ab5b"

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/ListInstanceUpdateRequest.xml"
title="Update List request example"
type="xml" %}

### 3.4 Update List response ###

#### http response & headers ####
```
HTTP/1.1 200 OK
Date:Tue, 24 Jul 2018 10:00:02 GMT
Last-Modified:2018-07-24T10:00:02+00:00
ETag: W/"3de1a085-95f3-43d2-be3c-aa60b6b3da85”
Content-Type:application/xml+fhir

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/ListInstanceUpdateResponse.xml"
title="Update List response example"
type="xml" %}

### 3.5 Delete Condition (B) request ###

#### http request & headers ####
```
PUT https://clinicals.spineservices.nhs.uk/STU3/Condition/13aec731-02c5-42a2-b863-de889479e777
 Authorization:Bearer [jwt_token_string]
 InteractionID:urn:nhs:names:services:flagserver
 If-Match:W/"cf8e1249-dfa6-4003-9745-d1b213008c95"

```
The only material difference between this request and Delete Condition (A) request will be time/order of receipt, and in the JWT payload.  

#### http body ####
As example above

### 3.6 Delete Condition (B) response ###

#### http response & headers ####
```
HTTP/1.1 409 CONFLICT
Date:Tue, 24 Jul 2018 10:10:02 GMT
Content-Type:application/xml+fhir

```

#### http body ####
```
<!-- Spine-operationOutcome-1 instance -->
<OperationOutcome xmlns="http://hl7.org/fhir">
    <id value="3ca2a2cb-b663-4ae9-b650-7cf4a23487ec"/>
    <meta>
        <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/Spine-OperationOutcome-1"/>
    </meta>
    <issue>
        <severity value="error"/>
        <code value="forbidden"/>
        <details>
            <coding>
                <system value="https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1"/>
                <code value="CONFLICT"/>
                <display value="Conflict"/>
            </coding>
        </details>
    </issue>
</OperationOutcome>

```
