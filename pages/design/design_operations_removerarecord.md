---
title: Operation | Remove RA Record
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_operations_removerarecord.html
summary: Remove RA Record operation describes the operation required to remove (soft delete) a Reasonable Adjustment Flag entirely, including all Adjustments, Impairments and Consents on the Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## Remove RA Record ##

'Remove RA Record' is an extended operation to efficiently close all active Reasonable Adjustment resources for a Patient.

In FHIR, the extended operations paradigm is defined at [Operations](http://hl7.org/fhir/operations.html). Each operation is specified via an instance of an operationDefinion resource.

Here:

|---------------:|-----------:|
| operation name | removerarecord |
| context        | server     |
| parameters     | NHSNumber, RemovalReason |

'server' context entails operation execution is invoked at the FHIR Server baseURL. Invocation syntax, in this case, specifies POST to the baseURL, the operation called by name with $ suffix

## Remove RA Record Invocation ##

Remove RA Record operation can be invoked directly or can be triggered by removal of Consent (to record Reasonable Adjustment information).

### http request ###
```
POST https://clinicals.spineservices.nhs.uk/STU3/$removerarecord /HTTP1.1
```
### body ###
The operation request body is a multi-part Parameter resource, containing the NHS Number of the Patient requiring their Reasonable Adjustment Flag removed, and optionally a RemovalReason where given

Examples of this operation interaction are available at [Remove RA Record](/design_usecases_RemoveRARecord.html)

## Remove RA Record Interaction ##

Interaction diagram outlining:
* operation request and 'in' parameters.
* pseudocode description of server-side actions (happy-path) 
* operation response

<img src="images/sequenceDiagrams/RemoveFlag.png">

```
$removerarecord
(In pseudocode:)

GET Flags WHERE
  subject=[NHS#]
  status=active
  category=RAFlag

Foreach Flag in searchset, 
    Update status=>inactive & removalReason=>[RemovalReason]

GET Consent WHERE
  subject=[NHS#]
  status=active
  category=RAFlag

Foreach Consent in searchset, 
    Update status=>inactive & removalReason=>[RemovalReason]

GET List WHERE
  subject=[NHS#]
  status=current
  category=[RAFlagCode]

Foreach Condition on List, 
    Update Condition.clinicalstatus=>inactive &
    Update List.entry.deleted=>true
```

## OperationDefinition ##

The OperationDefinition of [removerarecord](/explore_removeflag_operation.html) defines the in and out parameters for this operation and their structure and content.
