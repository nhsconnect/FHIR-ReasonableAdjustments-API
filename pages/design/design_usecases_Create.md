---
title: Create Use Cases
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_Create.html
summary: Create Use Cases describes the http request response behaviour of the endpoints and methods supported by the FHIR&reg; Reasonable Adjustments API to Create resources
---
{% include custom/search.warnbanner.html %}

## Create Use Cases

This page specifies the Create/POST use cases to be supported by the FHIR&reg; Reasonable Adjustments API.

### Consent

#### Summary:
Patient wishes to record Consent. Practitioner records Consent information in RA record


#### Main

* Patient consents to record RA Flag  
  * Practitioner creates new RARecord for Patient (by recording Consent)  
  * Practitioner records Patient consented to record RA info  
    * ClientSystem captures and structures Consent information as new RARecord Consent-1 resource
* Practitioner commits RARecord  
    * ClientSystem submits Create Consent request  
      * ServerSystem submits Create Consent response  

#### Examples

##### Http request

```
POST https://clinicals.spineservices.nhs.uk/STU3/Consent HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 0e577f8b-21ca-4e94-9ff1-f2c766cfb2d2
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.write:1
```

##### Request body - xml

```xml
<Consent xmlns="http://hl7.org/fhir">
    <status value="active"/>
    <category>
        <coding>
            <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-FlagCategory-1"/>
            <code value="NRAF"/>
            <display value="National Reasonable Adjustments Flag"/>
        </coding>
    </category>
    <patient>
        <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
    </patient>
    <policy>
        <authority value="https://www.gov.uk/"/>
        <uri value="https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.pdf"/>
    </policy>
    <purpose>
        <system value="https://snomed.info/sct"/>
        <code value="370856009"/>
        <display value="Limiting access to confidential patient information"/>
    </purpose>
</Consent>
```

##### Request body - json

```json
{
    "resourceType": "Consent",
    "status": "active",
    "category":  [
        {
            "coding":  [
                {
                    "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-FlagCategory-1",
                    "code": "NRAF",
                    "display": "National Reasonable Adjustments Flag"
                }
            ]
        }
    ],
    "patient": {
        "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
    },
    "policy":  [
        {
            "authority": "https://www.gov.uk/",
            "uri": "https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.pdf"
        }
    ],
    "purpose":  [
        {
            "system": "https://snomed.info/sct",
            "code": "370856009",
            "display": "Limiting access to confidential patient information"
        }
    ]
}

```

##### Http response

```
HTTP/1.1 201 Created
Date: Tue, 11 Apr 2023 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Consent/3408b2c7-e5aa-4578-87ca-48db8ffddb4a/_history/1c0193b2-1681-4ddc-a435-f78e94f85efd 
ETag: W/"1c0193b2-1681-4ddc-a435-f78e94f85efd”
Content-Type: application/fhir+xml
```

##### Response body - xml

```xml
<Bundle xmlns="http://hl7.org/fhir">
    <id value="13539d38-540c-4a1f-b0b3-c8ea23723aa8"/>
    <type value="searchset"/>
    <total value="1"/>
    <link>
        <relation value="self"/>
        <url value="https://clinicals.spineservices.nhs.uk/STU3/Consent?patient=999999998&amp;status=current&amp;code=http://snomed.info/sct|1094391000000102&amp;_format=xml"/>
   </link>
    <entry>
        <fullUrl value="https://clinicals.spineservices.nhs.uk/STU3/Consent/3408b2c7-e5aa-4578-87ca-48db8ffddb4a"/>
        <resource>
            <Consent xmlns="http://hl7.org/fhir">
                <id value="3408b2c7-e5aa-4578-87ca-48db8ffddb4a"/>
                <meta>
                    <versionId value="1c0193b2-1681-4ddc-a435-f78e94f85efd"/>
                    <lastUpdated value="2023-04-11T11:00:00+00:00"/>
                </meta>
                <contained>
                    <Provenance>
                        <target>
                            <reference value="#"/>
                        </target>
                        <recorded value="2023-04-11T11:00:00+00:00"/>
                        <activity>
                                <system value="http://hl7.org/fhir/v3/DataOperation"/>
                                <code value="CREATE"/>
                                <display value="create"/>
                        </activity>
                        <agent>
                            <role>
                                <coding>
                                    <system value="https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1"/>
                                    <code value="R0260"/>
                                    <display value="General Medical Practitioner"/>
                                </coding>
                            </role>
                            <whoReference>
                                <reference value="https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9"/>
                                <display value="Dr.D"/>
                            </whoReference>
                            <onBehalfOfReference>
                                <reference value="https://directory.spineservices.nhs.uk/STU3/Organization/a3e5i7"/>
                                <display value="Some GP Clinic"/>
                            </onBehalfOfReference>
                        </agent>
                    </Provenance>
                </contained>
                <status value="active"/>
                <category>
                    <coding>
                        <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-FlagCategory-1"/>
                        <code value="NRAF"/>
                        <display value="National Reasonable Adjustments Flag"/>
                    </coding>
                </category>
                <patient>
                    <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
                </patient>
                <policy>
                    <authority value="https://www.gov.uk/"/>
                    <uri value="https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.pdf"/>
                </policy>
                <purpose>
                    <system value="https://snomed.info/sct"/>
                    <code value="370856009"/>
                    <display value="Limiting access to confidential patient information"/>
                </purpose>
            </Consent>
        </resource>
        <search>
          <mode value="match"/>
        </search>
    </entry>
</Bundle>
```

##### Response body - json

```json


{
    "resourceType": "Bundle",
    "id": "13539d38-540c-4a1f-b0b3-c8ea23723aa8",
    "type": "searchset",
    "total": 1,
    "link":  [
        {
            "relation": "self",
            "url": "https://clinicals.spineservices.nhs.uk/STU3/Consent?patient=999999998&status=current&code=http://snomed.info/sct|1094391000000102&_format=xml"
        }
    ],
    "entry":  [
        {
            "fullUrl": "https://clinicals.spineservices.nhs.uk/STU3/Consent/3408b2c7-e5aa-4578-87ca-48db8ffddb4a",
            "resource": {
                "resourceType": "Consent",
                "id": "3408b2c7-e5aa-4578-87ca-48db8ffddb4a",
                "meta": {
                    "versionId": "1c0193b2-1681-4ddc-a435-f78e94f85efd",
                    "lastUpdated": "2023-04-11T11:00:00+00:00"
                },
                "contained":  [
                    {
                        "resourceType": "Provenance",
                        "target":  [
                            {
                                "reference": "#"
                            }
                        ],
                        "recorded": "2023-04-11T11:00:00+00:00",
                        "activity": {
                            "system": "http://hl7.org/fhir/v3/DataOperation",
                            "code": "CREATE",
                            "display": "create"
                        },
                        "agent":  [
                            {
                                "role":  [
                                    {
                                        "coding":  [
                                            {
                                                "system": "https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1",
                                                "code": "R0260",
                                                "display": "General Medical Practitioner"
                                            }
                                        ]
                                    }
                                ],
                                "whoReference": {
                                    "reference": "https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9",
                                    "display": "Dr.D"
                                },
                                "onBehalfOfReference": {
                                    "reference": "https://directory.spineservices.nhs.uk/STU3/Organization/a3e5i7",
                                    "display": "Some GP Clinic"
                                }
                            }
                        ]
                    }
                ],
                "status": "active",
                "category":  [
                    {
                        "coding":  [
                            {
                                "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-FlagCategory-1",
                                "code": "NRAF",
                                "display": "National Reasonable Adjustments Flag"
                            }
                        ]
                    }
                ],
                "patient": {
                    "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
                },
                "policy":  [
                    {
                        "authority": "https://www.gov.uk/",
                        "uri": "https://www.gov.uk/government/uploads/system/uploads/attachment_data/file/535024/data-security-review.pdf"
                    }
                ],
                "purpose":  [
                    {
                        "system": "https://snomed.info/sct",
                        "code": "370856009",
                        "display": "Limiting access to confidential patient information"
                    }
                ]
            },
            "search": {
                "mode": "match"
            }
        }
    ]
}


```

### Flag

#### Summary:
Patient wishes to record Adjustment. Practitioner records Adjustment information in RA record


#### Main

* Patient wishes to record an Adjustment
  * Practitioner records Adjustment info
    * ClientSystem captures and structures Consent information as new RARecord Flag-1 resource
* Practitioner commits RARecord
    * ClientSystem submits Create Adjustment request
      * ServerSystem submits Create Adjustment response

#### Examples

##### Http request

```
POST https://clinicals.spineservices.nhs.uk/STU3/Flag HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 6337a8ca-1951-441e-81d8-7c61e31c5fa5
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1
```


##### Request body - xml

```xml
<Flag xmlns="http://hl7.org/fhir">
    <extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-AdjustmentCategory-1">
        <valueCodeableConcept>
            <coding>
                <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-AdjustmentCategory-1"/>
                <code value="001"/>
                <display value="Communication support"/>
            </coding>
        </valueCodeableConcept>
    </extension>
    <status value="active"/>
    <category>
        <coding>
            <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-FlagCategory-1"/>
            <code value="NRAF"/>
            <display value="National Reasonable Adjustments Flag"/>
        </coding>
    </category>
    <code>
        <coding>
            <system value="https://snomed.info/sct"/>
            <code value="796161000000101"/>
            <display value="Requires information in Easyread"/>
        </coding>
    </code>
    <subject>
            <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
    </subject>
</Flag>
```

##### Request body - json

```json
{
    "resourceType": "Flag",
    "extension":  [
        {
            "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-AdjustmentCategory-1",
            "valueCodeableConcept": {
                "coding":  [
                    {
                        "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-AdjustmentCategory-1",
                        "code": "001",
                        "display": "Communication support"
                    }
                ]
            }
        }
    ],
    "status": "active",
    "category":  [
        {
            "coding":  [
                {
                    "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-FlagCategory-1",
                    "code": "NRAF",
                    "display": "National Reasonable Adjustments Flag"
                }
            ]
        }
    ],
    "code": {
        "coding":  [
            {
                "system": "https://snomed.info/sct",
                "code": "796161000000101",
                "display": "Requires information in Easyread"
            }
        ]
    },
    "subject": {
        "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
    }
}

```

##### Http response

```
HTTP/1.1 201 Created
Date: Tue, 11 Apr 2023 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/Flag/c939c9b8-2559-499e-99a9-c8b0bdbe1750/_history/1b1770be-64be-4844-bc87-f714b50a2378 
ETag: W/"1b1770be-64be-4844-bc87-f714b50a2378”
Content-Type: application/fhir+xml
```


##### Response body - xml

```xml
<Bundle xmlns="http://hl7.org/fhir">
    <id value="cecf0b04-6b5c-4c76-8aa2-80bc032f924d"/>
    <type value="searchset"/>
    <total value="1"/>
    <link>
        <relation value="self"/>
        <url value="https://clinicals.spineservices.nhs.uk/STU3/Flag?patient=999999998&amp;status=current&amp;code=http://snomed.info/sct|1094391000000102&amp;_format=xml"/>
   </link>
    <entry>
        <fullUrl value="https://clinicals.spineservices.nhs.uk/STU3/Flag/c939c9b8-2559-499e-99a9-c8b0bdbe1750"/>
        <resource>
            <Flag xmlns="http://hl7.org/fhir">
                <id value="c939c9b8-2559-499e-99a9-c8b0bdbe1750"/>
                <meta>
                    <versionId value="1b1770be-64be-4844-bc87-f714b50a2378"/>
                    <lastUpdated value="2023-04-11T11:00:00+00:00"/>
                </meta>
                <contained>
                    <Provenance>
                        <target>
                            <reference value="#"/>
                        </target>
                        <recorded value="2023-04-11T11:00:00+00:00"/>
                        <activity>
                                <system value="http://hl7.org/fhir/v3/DataOperation"/>
                                <code value="CREATE"/>
                                <display value="create"/>
                        </activity>
                        <agent>
                            <role>
                                <coding>
                                    <system value="https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1"/>
                                    <code value="R0260"/>
                                    <display value="General Medical Practitioner"/>
                                </coding>
                            </role>
                            <whoReference>
                                <reference value="https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9"/>
                                <display value="Dr.D"/>
                            </whoReference>
                            <onBehalfOfReference>
                                <reference value="https://directory.spineservices.nhs.uk/STU3/Organization/a3e5i7"/>
                                <display value="Some GP Clinic"/>
                            </onBehalfOfReference>
                        </agent>
                    </Provenance>

                </contained>
                <extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-AdjustmentCategory-1">
                    <valueCodeableConcept>
                        <coding>
                            <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-AdjustmentCategory-1"/>
                            <code value="001"/>
                            <display value="Communication support"/>
                        </coding>
                    </valueCodeableConcept>
                </extension>
                <status value="active"/>
                <category>
                    <coding>
                        <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-FlagCategory-1"/>
                        <code value="NRAF"/>
                        <display value="National Reasonable Adjustments Flag"/>
                    </coding>
                </category>
                <code>
                    <coding>
                        <system value="https://snomed.info/sct"/>
                        <code value="796161000000101"/>
                        <display value="Requires information in Easyread"/>
                    </coding>
                </code>
                <subject>
                        <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
                </subject>
            </Flag>
        </resource>
        <search>
          <mode value="match"/>
        </search>
    </entry>
</Bundle>
```

##### Response body - json

```json


{
    "resourceType": "Bundle",
    "id": "cecf0b04-6b5c-4c76-8aa2-80bc032f924d",
    "type": "searchset",
    "total": 1,
    "link":  [
        {
            "relation": "self",
            "url": "https://clinicals.spineservices.nhs.uk/STU3/Flag?patient=999999998&status=current&code=http://snomed.info/sct|1094391000000102&_format=xml"
        }
    ],
    "entry":  [
        {
            "fullUrl": "https://clinicals.spineservices.nhs.uk/STU3/Flag/c939c9b8-2559-499e-99a9-c8b0bdbe1750",
            "resource": {
                "resourceType": "Flag",
                "id": "c939c9b8-2559-499e-99a9-c8b0bdbe1750",
                "meta": {
                    "versionId": "1b1770be-64be-4844-bc87-f714b50a2378",
                    "lastUpdated": "2023-04-11T11:00:00+00:00"
                },
                "contained":  [
                    {
                        "resourceType": "Provenance",
                        "target":  [
                            {
                                "reference": "#"
                            }
                        ],
                        "recorded": "2023-04-11T11:00:00+00:00",
                        "activity": {
                            "system": "http://hl7.org/fhir/v3/DataOperation",
                            "code": "CREATE",
                            "display": "create"
                        },
                        "agent":  [
                            {
                                "role":  [
                                    {
                                        "coding":  [
                                            {
                                                "system": "https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1",
                                                "code": "R0260",
                                                "display": "General Medical Practitioner"
                                            }
                                        ]
                                    }
                                ],
                                "whoReference": {
                                    "reference": "https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9",
                                    "display": "Dr.D"
                                },
                                "onBehalfOfReference": {
                                    "reference": "https://directory.spineservices.nhs.uk/STU3/Organization/a3e5i7",
                                    "display": "Some GP Clinic"
                                }
                            }
                        ]
                    }
                ],
                "extension":  [
                    {
                        "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-AdjustmentCategory-1",
                        "valueCodeableConcept": {
                            "coding":  [
                                {
                                    "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-AdjustmentCategory-1",
                                    "code": "001",
                                    "display": "Communication support"
                                }
                            ]
                        }
                    }
                ],
                "status": "active",
                "category": {
                    "coding":  [
                        {
                            "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-FlagCategory-1",
                            "code": "NRAF",
                            "display": "National Reasonable Adjustments Flag"
                        }
                    ]
                },
                "code": {
                    "coding":  [
                        {
                            "system": "https://snomed.info/sct",
                            "code": "796161000000101",
                            "display": "Requires information in Easyread"
                        }
                    ]
                },
                "subject": {
                    "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
                }
            },
            "search": {
                "mode": "match"
            }
        }
    ]
}



```

### List

#### Summary:
Patient wishes to record Impairment. Practitioner records Impairment information in RA record


#### Main

* Patient wishes to record an Impairment
  * Practitioner records Impairment info
    * ClientSystem captures and structures Impairment information as new RARecord Condition-1 resource
* Practitioner commits RARecord
    * ClientSystem submits Create Impairment request
      * ServerSystem submits Create Impairment response

#### Examples

##### Http request

```
POST https://clinicals.spineservices.nhs.uk/STU3/List HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 47d46a8f-d6b5-4011-aad4-6d198efe2d16
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
```


##### Request body - xml

```xml
<Condition xmlns="http://hl7.org/fhir">
    <clinicalStatus value="active"/>
    <category>
        <coding>
            <system value="https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-ConditionCategory-1"/>
            <code value="issue"/>
            <display value="Issue"/>
        </coding>
    </category>
        <code>
            <coding>
                <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-ConditionCode-1"/>
                <code value="5"/>
                <display value="Learning or understanding or concentrating"/>
            </coding>
        </code>
    <subject>
        <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
    </subject>
</Condition>
```

##### Request body - json

```json
{
    "resourceType": "Condition",
    "clinicalStatus": "active",
    "category":  [
        {
            "coding":  [
                {
                    "system": "https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-ConditionCategory-1",
                    "code": "issue",
                    "display": "Issue"
                }
            ]
        }
    ],
    "code": {
        "coding":  [
            {
                "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-ConditionCode-1",
                "code": "5",
                "display": "Learning or understanding or concentrating"
            }
        ]
    },
    "subject": {
        "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
    }
}

```

##### Http response

```
HTTP/1.1 201 Created
Date: Tue, 11 Apr 2023 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/List/7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82/_history/9ab8be87-a98a-498b-a6ce-f1a55a60d1d2 
ETag: W/"9ab8be87-a98a-498b-a6ce-f1a55a60d1d2”
Content-Type: application/fhir+xml
```


##### Response body - xml

```xml
<Bundle xmlns="http://hl7.org/fhir">
    <id value="65662a62-08dc-4bbe-970e-51d44ab6a8e4"/>
    <type value="searchset"/>
    <total value="1"/>
    <link>
        <relation value="self"/>
        <url value="https://clinicals.spineservices.nhs.uk/STU3/List?patient=999999998&amp;status=current&amp;code=http://snomed.info/sct|1094391000000102&amp;_format=xml"/>
   </link>
    <entry>
        <fullUrl value="https://clinicals.spineservices.nhs.uk/STU3/List/7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82"/>
        <resource>
            <List xmlns="http://hl7.org/fhir">
                <id value="7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82"/>
                <meta>
                    <versionId value="9ab8be87-a98a-498b-a6ce-f1a55a60d1d2"/>
                    <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"/>
                </meta>
                <contained>
                    <Condition xmlns="http://hl7.org/fhir">
                        <clinicalStatus value="active"/>
                        <category>
                            <coding>
                                <system value="https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-ConditionCategory-1"/>
                                <code value="issue"/>
                                <display value="Issue"/>
                            </coding>
                        </category>
                            <code>
                                <coding>
                                    <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-ConditionCode-1"/>
                                    <code value="5"/>
                                    <display value="Learning or understanding or concentrating"/>
                                </coding>
                            </code>
                        <subject>
                            <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
                        </subject>
                    </Condition>
                </contained>
                <contained>
                    <Provenance>
                        <target>
                            <reference value="#"/>
                        </target>
                        <recorded value="2023-04-11T11:00:00+00:00"/>
                        <activity>
                                <system value="http://hl7.org/fhir/v3/DataOperation"/>
                                <code value="CREATE"/>
                                <display value="create"/>
                        </activity>
                        <agent>
                            <role>
                                <coding>
                                    <system value="https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1"/>
                                    <code value="R0260"/>
                                    <display value="General Medical Practitioner"/>
                                </coding>
                            </role>
                            <whoReference>
                                <reference value="https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9"/>
                                <display value="Dr.D"/>
                            </whoReference>
                            <onBehalfOfReference>
                                <reference value="https://directory.spineservices.nhs.uk/STU3/Organization/a3e5i7"/>
                                <display value="Some GP Clinic"/>
                            </onBehalfOfReference>
                        </agent>
                    </Provenance>
                </contained>
                <status value="current"/>
                <mode value="changes"/>
                <title value="Reasonable Adjustment List"/>
                <code>
                    <coding>
                        <system value="http://snomed.info/sct"/>
                        <code value="1094391000000102"/>
                        <display value="Reasonable adjustments for health and care access"/>
                    </coding>
                </code>
                <subject>
                    <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
                </subject>
                <date value="2023-04-11T11:00:00+00:00"/>
                <entry>
                    <deleted value="false"/>
                    <date value="2023-04-11T11:00:00+00:00"/>
                    <item>
                        <reference value="urn:uuid:[id uuid]"/>
                    </item>
                </entry>
                <entry>
                    <deleted value="false"/>
                    <date value="2023-04-11T11:00:00+00:00"/>
                    <item>
                        <reference value="urn:uuid:[id uuid]"/>
                    </item>
                </entry>
            </List>
        </resource>
        <search>
          <mode value="match"/>
        </search>
    </entry>
</Bundle>

```

##### Response body - json

```json


{
    "resourceType": "Bundle",
    "id": "65662a62-08dc-4bbe-970e-51d44ab6a8e4",
    "type": "searchset",
    "total": 1,
    "link":  [
        {
            "relation": "self",
            "url": "https://clinicals.spineservices.nhs.uk/STU3/List?patient=999999998&status=current&code=http://snomed.info/sct|1094391000000102&_format=xml"
        }
    ],
    "entry":  [
        {
            "fullUrl": "https://clinicals.spineservices.nhs.uk/STU3/List/7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82",
            "resource": {
                "resourceType": "List",
                "id": "7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82",
                "meta": {
                    "versionId": "9ab8be87-a98a-498b-a6ce-f1a55a60d1d2",
                    "profile":  [
                        "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"
                    ]
                },
                "contained":  [
                    {
                        "resourceType": "Condition",
                        "clinicalStatus": "active",
                        "category":  [
                            {
                                "coding":  [
                                    {
                                        "system": "https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-ConditionCategory-1",
                                        "code": "issue",
                                        "display": "Issue"
                                    }
                                ]
                            }
                        ],
                        "code": {
                            "coding":  [
                                {
                                    "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-ConditionCode-1",
                                    "code": "5",
                                    "display": "Learning or understanding or concentrating"
                                }
                            ]
                        },
                        "subject": {
                            "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
                        }
                    },
                    {
                        "resourceType": "Provenance",
                        "target":  [
                            {
                                "reference": "#"
                            }
                        ],
                        "recorded": "2023-04-11T11:00:00+00:00",
                        "activity": {
                            "system": "http://hl7.org/fhir/v3/DataOperation",
                            "code": "CREATE",
                            "display": "create"
                        },
                        "agent":  [
                            {
                                "role":  [
                                    {
                                        "coding":  [
                                            {
                                                "system": "https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1",
                                                "code": "R0260",
                                                "display": "General Medical Practitioner"
                                            }
                                        ]
                                    }
                                ],
                                "whoReference": {
                                    "reference": "https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9",
                                    "display": "Dr.D"
                                },
                                "onBehalfOfReference": {
                                    "reference": "https://directory.spineservices.nhs.uk/STU3/Organization/a3e5i7",
                                    "display": "Some GP Clinic"
                                }
                            }
                        ]
                    }
                ],
                "status": "current",
                "mode": "changes",
                "title": "Reasonable Adjustment List",
                "code": {
                    "coding":  [
                        {
                            "system": "http://snomed.info/sct",
                            "code": "1094391000000102",
                            "display": "Reasonable adjustments for health and care access"
                        }
                    ]
                },
                "subject": {
                    "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
                },
                "date": "2023-04-11T11:00:00+00:00",
                "entry":  [
                    {
                        "deleted": false,
                        "date": "2023-04-11T11:00:00+00:00",
                        "item": {
                            "reference": "urn:uuid:[id uuid]"
                        }
                    },
                    {
                        "deleted": false,
                        "date": "2023-04-11T11:00:00+00:00",
                        "item": {
                            "reference": "urn:uuid:[id uuid]"
                        }
                    }
                ]
            },
            "search": {
                "mode": "match"
            }
        }
    ]
}


```


### UnderlyingConditions

#### Summary:
Patient wishes to record Underlying Condition. Practitioner records Underlying Condition information in RA record


#### Main

* Patient wishes to record an Underlying Condition
  * Practitioner records Underlying Condition info
    * ClientSystem captures and structures Underlying Condition information as new RARecord Condition-1 resource
* Practitioner commits RARecord
    * ClientSystem submits Create Underlying Condition request
      * ServerSystem submits Create Underlying Condition response

#### Examples

##### Http request

```
POST https://clinicals.spineservices.nhs.uk/STU3/UnderlyingConditions HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 
770bd026-2093-45bb-a944-10cc9e83a5cb
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:UnderlyingConditions.write:1
```


##### Request body - xml

```xml
<Condition xmlns="http://hl7.org/fhir">
    <clinicalStatus value="active"/>
    <category>
        <coding>
            <system value="https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-ConditionCategory-1"/>
            <code value="issue"/>
            <display value="Issue"/>
        </coding>
    </category>
        <code>
            <coding>
                <system value="https://snomed.info/sct"/>
                <code value="73618009"/>
                <display value="Autistic spectrum disorder with isolated skills"/>
            </coding>
        </code>
    <subject>
        <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
    </subject>
</Condition>
```

##### Request body - json

```json
{
    "resourceType": "Condition",
    "clinicalStatus": "active",
    "category":  [
        {
            "coding":  [
                {
                    "system": "https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-ConditionCategory-1",
                    "code": "issue",
                    "display": "Issue"
                }
            ]
        }
    ],
    "code": {
        "coding":  [
            {
                "system": "https://snomed.info/sct",
                "code": "73618009",
                "display": "Autistic spectrum disorder with isolated skills"
            }
        ]
    },
    "subject": {
        "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
    }
}

```

##### Http response

```
HTTP/1.1 201 Created
Date: Tue, 11 Apr 2023 11:00:00 GMT
Last-Modified:2018-07-23T11:00:00+00:00
Location: https://clinicals.spineservices.nhs.uk/STU3/UnderlyingConditions/fd756ccc-e6d2-4e40-991d-b022abc20aa0/_history/616201a0-1364-427b-999f-750691b08989 
ETag: W/"616201a0-1364-427b-999f-750691b08989”
Content-Type: application/fhir+xml
```


##### Response body - xml

```xml
<Bundle xmlns="http://hl7.org/fhir">
    <id value="0f09b412-9719-42f0-ae0d-392766e6180f"/>
    <type value="searchset"/>
    <total value="1"/>
    <link>
        <relation value="self"/>
        <url value="https://clinicals.spineservices.nhs.uk/STU3/UnderlyingConditions?patient=999999998&amp;status=current&amp;code=http://snomed.info/sct|1094391000000102&amp;_format=xml"/>
   </link>
    <entry>
        <fullUrl value="https://clinicals.spineservices.nhs.uk/STU3/UnderlyingConditions/fd756ccc-e6d2-4e40-991d-b022abc20aa0"/>
        <resource>
            <List xmlns="http://hl7.org/fhir">
                <id value="fd756ccc-e6d2-4e40-991d-b022abc20aa0"/>
                <meta>
                    <versionId value="616201a0-1364-427b-999f-750691b08989"/>
                    <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"/>
                </meta>
                <contained>
                    <Condition xmlns="http://hl7.org/fhir">
                        <clinicalStatus value="active"/>
                        <category>
                            <coding>
                                <system value="https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-ConditionCategory-1"/>
                                <code value="issue"/>
                                <display value="Issue"/>
                            </coding>
                        </category>
                            <code>
                                <coding>
                                    <system value="https://snomed.info/sct"/>
                                    <code value="73618009"/>
                                    <display value="Autistic spectrum disorder with isolated skills"/>
                                </coding>
                            </code>
                        <subject>
                            <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
                        </subject>
                    </Condition>
                </contained>
                <contained>
                    <Provenance>
                        <target>
                            <reference value="#"/>
                        </target>
                        <recorded value="2023-04-11T11:00:00+00:00"/>
                        <activity>
                                <system value="http://hl7.org/fhir/v3/DataOperation"/>
                                <code value="CREATE"/>
                                <display value="create"/>
                        </activity>
                        <agent>
                            <role>
                                <coding>
                                    <system value="https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1"/>
                                    <code value="R0260"/>
                                    <display value="General Medical Practitioner"/>
                                </coding>
                            </role>
                            <whoReference>
                                <reference value="https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9"/>
                                <display value="Dr.D"/>
                            </whoReference>
                            <onBehalfOfReference>
                                <reference value="https://directory.spineservices.nhs.uk/STU3/Organization/a3e5i7"/>
                                <display value="Some GP Clinic"/>
                            </onBehalfOfReference>
                        </agent>
                    </Provenance>
                </contained>
                <status value="current"/>
                <mode value="changes"/>
                <title value="Reasonable Adjustment List"/>
                <code>
                    <coding>
                        <system value="http://snomed.info/sct"/>
                        <code value="1094391000000102"/>
                        <display value="Reasonable adjustments for health and care access"/>
                    </coding>
                </code>
                <subject>
                    <reference value="https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
                </subject>
                <date value="2023-04-11T11:00:00+00:00"/>
                <entry>
                    <deleted value="false"/>
                    <date value="2023-04-11T11:00:00+00:00"/>
                    <item>
                        <reference value="urn:uuid:[id uuid]"/>
                    </item>
                </entry>
                <entry>
                    <deleted value="false"/>
                    <date value="2023-04-11T11:00:00+00:00"/>
                    <item>
                        <reference value="urn:uuid:[id uuid]"/>
                    </item>
                </entry>
            </List>
        </resource>
        <search>
          <mode value="match"/>
        </search>
    </entry>
</Bundle>

```

##### Response body - json

```json


{
    "resourceType": "Bundle",
    "id": "0f09b412-9719-42f0-ae0d-392766e6180f",
    "type": "searchset",
    "total": 1,
    "link":  [
        {
            "relation": "self",
            "url": "https://clinicals.spineservices.nhs.uk/STU3/UnderlyingConditions?patient=999999998&status=current&code=http://snomed.info/sct|1094391000000102&_format=xml"
        }
    ],
    "entry":  [
        {
            "fullUrl": "https://clinicals.spineservices.nhs.uk/STU3/UnderlyingConditions/fd756ccc-e6d2-4e40-991d-b022abc20aa0",
            "resource": {
                "resourceType": "List",
                "id": "fd756ccc-e6d2-4e40-991d-b022abc20aa0",
                "meta": {
                    "versionId": "616201a0-1364-427b-999f-750691b08989",
                    "profile":  [
                        "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"
                    ]
                },
                "contained":  [
                    {
                        "resourceType": "Condition",
                        "clinicalStatus": "active",
                        "category":  [
                            {
                                "coding":  [
                                    {
                                        "system": "https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-ConditionCategory-1",
                                        "code": "issue",
                                        "display": "Issue"
                                    }
                                ]
                            }
                        ],
                        "code": {
                            "coding":  [
                                {
                                    "system": "https://snomed.info/sct",
                                    "code": "73618009",
                                    "display": "Autistic spectrum disorder with isolated skills"
                                }
                            ]
                        },
                        "subject": {
                            "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
                        }
                    },
                    {
                        "resourceType": "Provenance",
                        "target":  [
                            {
                                "reference": "#"
                            }
                        ],
                        "recorded": "2023-04-11T11:00:00+00:00",
                        "activity": {
                            "system": "http://hl7.org/fhir/v3/DataOperation",
                            "code": "CREATE",
                            "display": "create"
                        },
                        "agent":  [
                            {
                                "role":  [
                                    {
                                        "coding":  [
                                            {
                                                "system": "https://fhir.hl7.org.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1",
                                                "code": "R0260",
                                                "display": "General Medical Practitioner"
                                            }
                                        ]
                                    }
                                ],
                                "whoReference": {
                                    "reference": "https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9",
                                    "display": "Dr.D"
                                },
                                "onBehalfOfReference": {
                                    "reference": "https://directory.spineservices.nhs.uk/STU3/Organization/a3e5i7",
                                    "display": "Some GP Clinic"
                                }
                            }
                        ]
                    }
                ],
                "status": "current",
                "mode": "changes",
                "title": "Reasonable Adjustment List",
                "code": {
                    "coding":  [
                        {
                            "system": "http://snomed.info/sct",
                            "code": "1094391000000102",
                            "display": "Reasonable adjustments for health and care access"
                        }
                    ]
                },
                "subject": {
                    "reference": "https://demographics.spineservices.nhs.uk/STU3/Patient/999999998"
                },
                "date": "2023-04-11T11:00:00+00:00",
                "entry":  [
                    {
                        "deleted": false,
                        "date": "2023-04-11T11:00:00+00:00",
                        "item": {
                            "reference": "urn:uuid:[id uuid]"
                        }
                    },
                    {
                        "deleted": false,
                        "date": "2023-04-11T11:00:00+00:00",
                        "item": {
                            "reference": "urn:uuid:[id uuid]"
                        }
                    }
                ]
            },
            "search": {
                "mode": "match"
            }
        }
    ]
}


```

