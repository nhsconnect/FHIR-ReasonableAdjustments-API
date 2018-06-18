---
title: Interaction | Remove Flag
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_operations_removeflag.html
summary: Remove Flag operation describes interaction required to remove (soft delete) a Reasonable Adjustment Flag entirely, including all Adjustments, Impairments and Consents on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Remove Flag ##

'Remove Flag' is an extended operation to efficiently close all active Reasonable Adjustment resources for a Patient.

In FHIR, the extended operations paradigm is defined at [Operations](http://hl7.org/fhir/operations.html). Each operation is specified via an instance of an operationDefinion resource.

Here:

|---------------:|-----------:|
| operation name | removeflag |
| context        | server     |
| parameters     | NHSNumber, RemovalReason |

'server' context entails operation execution is invoked at the FHIR Server baseURL. Invocation syntax, in this case, specifies POST to the baseURL, the operation called by name with $ suffix

## 2 Remove Flag Invocation ##

### http request ###
```
POST https://clinicals.spineservices.nhs.uk/STU3/flagserver/$removeflag /HTTP1.1
```
### body ###
The operation request body is a multi-part Parameter resource, containing the NHS Number of the Patient requiring their Reasonable Adjustment Flag removed, and optionally a RemovalReason where given

#### XML parameter example ####
```
<Parameters>
    <parameter>
        <name value="removeflag"/>
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
      "name": "removeflag",
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

## 3 Remove Flag Interaction ##

Interaction diagram outlining:
* operation request and 'in' parameters.
* pseudocode description of server-side actions (happy-path) 
* operation response

```
Client                    Server
  |                         |
  | -> removeflag [NHS#,    |
  |          RemovalReason] |
  |                         |
  |                         | removeflag 
  |                         | (In pseudocode:)
  |                         | ================
  |                         | GET Flags WHERE
  |                         | 	subject=[NHS#]
  |                         | 	status=active
  |                         | 	category=RAFlag
  |                         | 
  |                         | Foreach Flag in searchset, Update status=>inactive & removalReason=>[RemovalReason] 
  |                         | 
  |                         | GET Consent WHERE
  |                         | 	subject=[NHS#]
  |                         | 	status=active
  |                         | 	category=RAFlag
  |                         | 
  |                         | Foreach Consent in searchset, Update status=>inactive & removalReason=>[RemovalReason] 
  |                         | 
  |                         | GET List WHERE
  |                         | 	subject=[NHS#]
  |                         | 	status=current
  |                         | 	category=[RAFlagCode]
  |                         | 
  |                         | Foreach Condition on List, Update Condition.clinicalstatus=>inactive 
  |                         | & Update List.entry.deleted=>true 
  |                         | 
  | <- http response &      |
  |    operation outcome    |   
```


