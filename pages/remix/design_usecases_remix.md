---
title: Interaction
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
 patient=[nhs#]&
 status=active&
 category=[RAFlag]&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver

```
### 1.2 Read Consent request - json example  ###

#### http request & headers ####

```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=[nhs#]&
 status=active&
 category=[RAFlag]&
 _format=xml HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver

```

#### http body ####
**None**

### 1.3 Read Consent response - xml example ###

#### http response & headers ####
```
HTTP/1.1 404 PATIENT NOT FOUND
Date:
ETag:
Location:
Last-Modified:
Content-Type:application/xml+fhir

```
**DQ:** Would you slap the full header & meta shebang in an OpOutcome?
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
Date:
ETag:
Location:
Last-Modified:
Content-Type:

```
**DQ:** Would you slap the full header & meta shebang in an OpOutcome?
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
#### http body ####

### 2.2 Read List response ###

#### http response & headers ####
#### http body ####

### 2.3 Read Conditions request ###

#### http request & headers ####
#### http body ####

### 2.4 Read Conditions response ###

#### http response & headers ####
#### http body ####


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
#### http body ####

### 3.2 Delete Condition (A) response ###

#### http response & headers ####
#### http body ####

### 3.3 Update List request ###

#### http request & headers ####
#### http body ####

### 3.4 Update List response ###

#### http response & headers ####
#### http body ####

### 3.5 Delete Condition (B) request ###

#### http request & headers ####
#### http body ####

### 3.6 Delete Condition (B) response ###

#### http response & headers ####
#### http body ####