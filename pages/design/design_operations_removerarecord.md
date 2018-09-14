---
title: Operation | Remove RA Record
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_operations_removerarecord.html
summary: Remove RA Record operation describes the operation required to remove (soft delete) a Reasonable Adjustment Flag entirely, including all Adjustments, Impairments and Consents on the Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Remove RA Record ##

'Remove RA Record' is an extended operation to efficiently close all active Reasonable Adjustment resources for a Patient.

In FHIR, the extended operations paradigm is defined at [Operations](http://hl7.org/fhir/operations.html). Each operation is specified via an instance of an operationDefinion resource.

Here:

|---------------:|-----------:|
| operation name | removerarecord |
| context        | server     |
| parameters     | NHSNumber, RemovalReason |

'server' context entails operation execution is invoked at the FHIR Server baseURL. Invocation syntax, in this case, specifies POST to the baseURL, the operation called by name with $ suffix

## 2 Remove RA Record Invocation ##

Remove RA Record operation can be invoked directly or can be triggered by removal of Consent (to record Reasonable Adjustment information).

### http request ###
```
POST https://clinicals.spineservices.nhs.uk/STU3/$removerarecord /HTTP1.1
```
### body ###
The operation request body is a multi-part Parameter resource, containing the NHS Number of the Patient requiring their Reasonable Adjustment Flag removed, and optionally a RemovalReason where given

#### XML parameter example ####
```
<Parameters>
    <parameter>
        <name value="removerarecord"/>
        <part>
            <name value="nhsNumber"/>
            <valueString value="999999998"/>
        </part>
        <part>
            <name value="removalReason"/>
                <valueCodeableConcept>
                    <coding>
                        <system value="https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-RemovalReason-1"/>
                        <code value="DoesntApply"/>
                        <display value="The Reasonable Adjustment Flag no longer applies to the patient"/>
                    </coding>
                </valueCodeableConcept>
            </part>
    </parameter>
</Parameters>
```
or 

#### JSON parameter example ####

```
{
  "resourceType": "Parameters",
  "parameter": [
    {
      "name": "removerarecord",
      "part": [
        {
          "name": "nhsNumber",
          "valueString": "999999998"
        },
        {
          "name": "removalReason",
          "valueCodeableConcept": {
            "coding": [
              {
                "system": "https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-RemovalReason-1",
                "code": "DoesntApply",
                "display": "The Reasonable Adjustment Flag no longer applies to the patient"
              }
            ]
          }
        }
      ]
    }
  ]
}
```

## 3 Remove RA Record Interaction ##

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

## 4 OperationDefinition ##

{% include important.html content="**Placeholder:** An OperationDefinition instance _will_ be provided for the $removerarecord operation." %}
