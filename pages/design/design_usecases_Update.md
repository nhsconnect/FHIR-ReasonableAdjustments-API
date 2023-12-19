---
title: Update Use Cases
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_Update.html
summary: Update Use Cases describes the http request response behaviour of the endpoints and methods supported by the FHIR&reg; Reasonable Adjustments API to Update resources
---
{% include custom/search.warnbanner.html %}

## Update Use Cases

This page specifies the Update(Delete)/PUT use cases to be supported by the FHIR&reg; Reasonable Adjustments API.

### Consent

#### Summary:
Patient wishes to remove Consent. Practitioner records Consent removed


#### Main

* Patient wishes to remove Consent
  * Practitioner records Consent removal and Removal reason
    * ClientSystem captures and structures Consent removal information
* Practitioner commits RARecord
    * ClientSystem submits Remove Consent request
      * ServerSystem submits Remove Consent response

#### Examples

##### Http request

```
PUT https://clinicals.spineservices.nhs.uk/STU3/Consent/3408b2c7-e5aa-4578-87ca-48db8ffddb4a HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 88a9fe4e-34cd-47d3-9da9-f426005e8902
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.write:1
If-Match: W/"1c0193b2-1681-4ddc-a435-f78e94f85efd"
```


##### Request body - xml

```xml

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
<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1" >
    <extension url="removalReason" >
        <valueCodeableConcept>
            <coding>
                <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1"/>
                <code value="Error"/>
                <display value="The Reasonable Adjustment Flag was created in error"/>
            </coding>
        </valueCodeableConcept>
    </extension>
    <extension url="supportingComment" >
        <valueString value="Reasonable Adjustment Flag was created in error" />
    </extension>
</extension>
<status value="inactive"/>
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
    "extension":  [
        {
            "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1",
            "extension":  [
                {
                    "url": "removalReason",
                    "valueCodeableConcept": {
                        "coding":  [
                            {
                                "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1",
                                "code": "Error",
                                "display": "The Reasonable Adjustment Flag was created in error"
                            }
                        ]
                    }
                },
                {
                    "url": "supportingComment",
                    "valueString": "Reasonable Adjustment Flag was created in error"
                }
            ]
        }
    ],
    "status": "inactive",
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
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Last-Modified: 2018-07-25T11:00:00+00:00
ETag: W/"[versionId uuid]”
Content-Type: application/fhir+xml
```

##### Response body - xml

```xml

<Consent xmlns="http://hl7.org/fhir">
<id value="3408b2c7-e5aa-4578-87ca-48db8ffddb4a"/>
<meta>
    <versionId value="5c14f6d4-ad1b-4df2-8c08-da271430f245"/>
    <lastUpdated value="2023-04-14T11:00:00+00:00"/>
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
<contained>
    <Provenance>
        <id value="7fa1ef30-81d9-4d6b-b24c-5d51ffa4092d"/>
        <target>
            <reference value="#"/>
        </target>
        <recorded value="2023-04-14T11:00:00+00:00"/>
        <activity>
                <system value="http://hl7.org/fhir/v3/DataOperation"/>
                <code value="UPDATE"/>
                <display value="revise"/>
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
<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1" >
    <extension url="removalReason" >
        <valueCodeableConcept>
            <coding>
                <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1"/>
                <code value="Error"/>
                <display value="The Reasonable Adjustment Flag was created in error"/>
            </coding>
        </valueCodeableConcept>
    </extension>
    <extension url="supportingComment" >
        <valueString value="Reasonable Adjustment Flag was created in error" />
    </extension>
</extension>
<status value="inactive"/>
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

##### Response body - json

```json


{
    "resourceType": "Consent",
    "id": "3408b2c7-e5aa-4578-87ca-48db8ffddb4a",
    "meta": {
        "versionId": "5c14f6d4-ad1b-4df2-8c08-da271430f245",
        "lastUpdated": "2023-04-14T11:00:00+00:00"
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
        },
        {
            "resourceType": "Provenance",
            "id": "7fa1ef30-81d9-4d6b-b24c-5d51ffa4092d",
            "target":  [
                {
                    "reference": "#"
                }
            ],
            "recorded": "2023-04-14T11:00:00+00:00",
            "activity": {
                "system": "http://hl7.org/fhir/v3/DataOperation",
                "code": "UPDATE",
                "display": "revise"
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
            "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1",
            "extension":  [
                {
                    "url": "removalReason",
                    "valueCodeableConcept": {
                        "coding":  [
                            {
                                "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1",
                                "code": "Error",
                                "display": "The Reasonable Adjustment Flag was created in error"
                            }
                        ]
                    }
                },
                {
                    "url": "supportingComment",
                    "valueString": "Reasonable Adjustment Flag was created in error"
                }
            ]
        }
    ],
    "status": "inactive",
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


### Flag

#### Summary:
Patient wishes to remove Adjustment. Practitioner records Adjustment removed


#### Main

* Patient wishes to remove an Adjustment
  * Practitioner records Adjustment removal and Removal reason
    * ClientSystem captures and structures Adjustment removal information
* Practitioner commits RARecord
    * ClientSystem submits Remove Adjustment request
      * ServerSystem submits Remove Adjustment response

#### Examples

##### Http request

```
PUT https://clinicals.spineservices.nhs.uk/STU3/Flag/c939c9b8-2559-499e-99a9-c8b0bdbe1750 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: ba2ba233-8929-4234-87a4-5092374409d9
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.write:1
If-Match: W/"1b1770be-64be-4844-bc87-f714b50a2378"
```


##### Request body - xml

```xml
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
<status value="inactive"/>
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
            "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1",
            "extension":  [
                {
                    "url": "removalReason",
                    "valueCodeableConcept": {
                        "coding":  [
                            {
                                "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1",
                                "code": "Error",
                                "display": "The Reasonable Adjustment Flag was created in error"
                            }
                        ]
                    }
                },
                {
                    "url": "supportingComment",
                    "valueString": "Requires Large Print rather than Easy Read"
                }
            ]
        },
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
    "status": "inactive",
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
}


```

##### Http response

```
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Last-Modified: 2018-07-25T11:00:00+00:00
ETag: W/"[versionId uuid]”
Content-Type: application/fhir+xml
```

##### Response body - xml

```xml
<Flag xmlns="http://hl7.org/fhir">
<id value="c939c9b8-2559-499e-99a9-c8b0bdbe1750"/>
<meta>
    <versionId value="5c14f6d4-ad1b-4df2-8c08-da271430f245"/>
    <lastUpdated value="2023-04-14T11:00:00+00:00"/>
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
<contained>
    <Provenance>
        <id value="7fa1ef30-81d9-4d6b-b24c-5d51ffa4092d"/>
        <target>
            <reference value="#"/>
        </target>
        <recorded value="2023-04-14T11:00:00+00:00"/>
        <activity>
                <system value="http://hl7.org/fhir/v3/DataOperation"/>
                <code value="UPDATE"/>
                <display value="revise"/>
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
<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1" >
    <extension url="removalReason" >
        <valueCodeableConcept>
            <coding>
                <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1"/>
                <code value="Error"/>
                <display value="The Reasonable Adjustment Flag was created in error"/>
            </coding>
        </valueCodeableConcept>
    </extension>
    <extension url="supportingComment" >
        <valueString value="Requires Large Print rather than Easy Read" />
    </extension>
</extension>
<extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-AdjustmentCategory-1">
    <valueCodeableConcept>
        <coding>
            <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-AdjustmentCategory-1"/>
            <code value="001"/>
            <display value="Communication support"/>
        </coding>
    </valueCodeableConcept>
</extension>
<status value="inactive"/>
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

##### Response body - json

```json


{
    "resourceType": "Flag",
    "id": "c939c9b8-2559-499e-99a9-c8b0bdbe1750",
    "meta": {
        "versionId": "5c14f6d4-ad1b-4df2-8c08-da271430f245",
        "lastUpdated": "2023-04-14T11:00:00+00:00"
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
        },
        {
            "resourceType": "Provenance",
            "id": "7fa1ef30-81d9-4d6b-b24c-5d51ffa4092d",
            "target":  [
                {
                    "reference": "#"
                }
            ],
            "recorded": "2023-04-14T11:00:00+00:00",
            "activity": {
                "system": "http://hl7.org/fhir/v3/DataOperation",
                "code": "UPDATE",
                "display": "revise"
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
            "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1",
            "extension":  [
                {
                    "url": "removalReason",
                    "valueCodeableConcept": {
                        "coding":  [
                            {
                                "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1",
                                "code": "Error",
                                "display": "The Reasonable Adjustment Flag was created in error"
                            }
                        ]
                    }
                },
                {
                    "url": "supportingComment",
                    "valueString": "Requires Large Print rather than Easy Read"
                }
            ]
        },
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
    "status": "inactive",
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
}


```


### List

#### Summary:
Patient wishes to remove Impairment. Practitioner records Impairment removed


#### Main

* Patient wishes to remove an Impairment
  * Practitioner records Impairment removal and Removal reason
    * ClientSystem captures and structures Impairment removal information
* Practitioner commits RARecord
    * ClientSystem submits Remove Impairment request
      * ServerSystem submits Remove Impairment response

#### Examples

##### Http request

```
PUT https://clinicals.spineservices.nhs.uk/STU3/List/7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: 215f26a8-0a44-43c6-8c01-57fd943f309c
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.write:1
If-Match: W/"9ab8be87-a98a-498b-a6ce-f1a55a60d1d2"
```


##### Request body - xml

```xml
<List xmlns="http://hl7.org/fhir">
    <id value="7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82"/>
    <meta>
        <versionId value="9ab8be87-a98a-498b-a6ce-f1a55a60d1d2"/>
        <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"/>
    </meta>
    <contained>
        <Condition xmlns="http://hl7.org/fhir">
            <id value="b93095f4-cf0a-492e-8513-10669d0ae256"/>
            <extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1" >
                <extension url="removalReason" >
                    <valueCodeableConcept>
                        <coding>
                            <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1"/>
                            <code value="Error"/>
                            <display value="The Reasonable Adjustment Flag was created in error"/>
                        </coding>
                    </valueCodeableConcept>
                </extension>
                <extension url="supportingComment" >
                    <valueString value="Reasonable Adjustment Flag was created in error" />
                </extension>
            </extension>
            
            <clinicalStatus value="inactive"/>
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
            <id value="3f72b305-5109-4360-ba98-473cb0a45957"/>
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
            <reference value="urn:uuid:b93095f4-cf0a-492e-8513-10669d0ae256"/>
        </item>
    </entry>
    <entry>
        <deleted value="false"/>
        <date value="2023-04-11T11:00:00+00:00"/>
        <item>
            <reference value="urn:uuid:3f72b305-5109-4360-ba98-473cb0a45957"/>
        </item>
    </entry>
</List>
```

##### Request body - json

```json


{
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
            "id": "b93095f4-cf0a-492e-8513-10669d0ae256",
            "extension":  [
                {
                    "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1",
                    "extension":  [
                        {
                            "url": "removalReason",
                            "valueCodeableConcept": {
                                "coding":  [
                                    {
                                        "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1",
                                        "code": "Error",
                                        "display": "The Reasonable Adjustment Flag was created in error"
                                    }
                                ]
                            }
                        },
                        {
                            "url": "supportingComment",
                            "valueString": "Reasonable Adjustment Flag was created in error"
                        }
                    ]
                }
            ],
            "clinicalStatus": "inactive",
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
            "id": "3f72b305-5109-4360-ba98-473cb0a45957",
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
                "reference": "urn:uuid:b93095f4-cf0a-492e-8513-10669d0ae256"
            }
        },
        {
            "deleted": false,
            "date": "2023-04-11T11:00:00+00:00",
            "item": {
                "reference": "urn:uuid:3f72b305-5109-4360-ba98-473cb0a45957"
            }
        }
    ]
}


```

##### Http response

```
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Last-Modified: 2018-07-25T11:00:00+00:00
ETag: W/"[versionId uuid]”
Content-Type: application/fhir+xml
```

##### Response body - xml

```xml
<List xmlns="http://hl7.org/fhir">
    <id value="7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82"/>
    <meta>
        <versionId value="917771c2-521c-422b-a1a5-1f16992cbd5c"/>
        <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"/>
    </meta>
    <contained>
        <Condition xmlns="http://hl7.org/fhir">
            <id value="b93095f4-cf0a-492e-8513-10669d0ae256"/>
            <extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1" >
                <extension url="removalReason" >
                    <valueCodeableConcept>
                        <coding>
                            <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1"/>
                            <code value="Error"/>
                            <display value="The Reasonable Adjustment Flag was created in error"/>
                        </coding>
                    </valueCodeableConcept>
                </extension>
                <extension url="supportingComment" >
                    <valueString value="Reasonable Adjustment Flag was created in error" />
                </extension>
            </extension>
            <clinicalStatus value="inactive"/>
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
            <id value="3f72b305-5109-4360-ba98-473cb0a45957"/>
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
    <contained>
        <Provenance>
            <id value="7fa1ef30-81d9-4d6b-b24c-5d51ffa4092d"/>
            <target>
                <reference value="#"/>
            </target>
            <recorded value="2023-04-14T11:00:00+00:00"/>
            <activity>
                    <system value="http://hl7.org/fhir/v3/DataOperation"/>
                    <code value="UPDATE"/>
                    <display value="revise"/>
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
        <deleted value="true"/>
        <date value="2023-04-11T11:00:00+00:00"/>
        <item>
            <reference value="urn:uuid:b93095f4-cf0a-492e-8513-10669d0ae256"/>
        </item>
    </entry>
    <entry>
        <deleted value="false"/>
        <date value="2023-04-11T11:00:00+00:00"/>
        <item>
            <reference value="urn:uuid:3f72b305-5109-4360-ba98-473cb0a45957"/>
        </item>
    </entry>
    <entry>
        <deleted value="false"/>
        <date value="2023-04-11T11:00:00+00:00"/>
        <item>
            <reference value="urn:uuid:7fa1ef30-81d9-4d6b-b24c-5d51ffa4092d"/>
        </item>
    </entry>
</List>
```

##### Response body - json

```json


{
    "resourceType": "List",
    "id": "7c2f6bb4-61e0-4dbb-9ce8-81761a4e6a82",
    "meta": {
        "versionId": "917771c2-521c-422b-a1a5-1f16992cbd5c",
        "profile":  [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"
        ]
    },
    "contained":  [
        {
            "resourceType": "Condition",
            "id": "b93095f4-cf0a-492e-8513-10669d0ae256",
            "extension":  [
                {
                    "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1",
                    "extension":  [
                        {
                            "url": "removalReason",
                            "valueCodeableConcept": {
                                "coding":  [
                                    {
                                        "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1",
                                        "code": "Error",
                                        "display": "The Reasonable Adjustment Flag was created in error"
                                    }
                                ]
                            }
                        },
                        {
                            "url": "supportingComment",
                            "valueString": "Reasonable Adjustment Flag was created in error"
                        }
                    ]
                }
            ],
            "clinicalStatus": "inactive",
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
            "id": "3f72b305-5109-4360-ba98-473cb0a45957",
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
        },
        {
            "resourceType": "Provenance",
            "id": "7fa1ef30-81d9-4d6b-b24c-5d51ffa4092d",
            "target":  [
                {
                    "reference": "#"
                }
            ],
            "recorded": "2023-04-14T11:00:00+00:00",
            "activity": {
                "system": "http://hl7.org/fhir/v3/DataOperation",
                "code": "UPDATE",
                "display": "revise"
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
            "deleted": true,
            "date": "2023-04-11T11:00:00+00:00",
            "item": {
                "reference": "urn:uuid:b93095f4-cf0a-492e-8513-10669d0ae256"
            }
        },
        {
            "deleted": false,
            "date": "2023-04-11T11:00:00+00:00",
            "item": {
                "reference": "urn:uuid:3f72b305-5109-4360-ba98-473cb0a45957"
            }
        },
        {
            "deleted": false,
            "date": "2023-04-11T11:00:00+00:00",
            "item": {
                "reference": "urn:uuid:7fa1ef30-81d9-4d6b-b24c-5d51ffa4092d"
            }
        }
    ]
}


```


### UnderlyingConditions

#### Summary:
Patient wishes to remove Underlying Condition. Practitioner records Underlying Condition removed


#### Main

* Patient wishes to remove an Underlying Condition
  * Practitioner records Underlying Condition removal and Removal reason
    * ClientSystem captures and structures Underlying Condition removal information as new RARecord Condition-1 resource
* Practitioner commits RARecord
    * ClientSystem submits Remove Underlying Condition request
      * ServerSystem submits Remove Underlying Condition response

#### Examples

##### Http request

```
PUT https://clinicals.spineservices.nhs.uk/STU3/UnderlyingConditions/fd756ccc-e6d2-4e40-991d-b022abc20aa0 HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: e1be37ea-a74e-4464-91e4-b000d2c743ec
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:UnderlyingConditions.write:1
If-Match: W/"616201a0-1364-427b-999f-750691b08989"
```


##### Request body - xml

```xml
<List xmlns="http://hl7.org/fhir">
    <id value="fd756ccc-e6d2-4e40-991d-b022abc20aa0"/>
    <meta>
        <versionId value="616201a0-1364-427b-999f-750691b08989"/>
        <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"/>
    </meta>
    <contained>
        <Condition xmlns="http://hl7.org/fhir">
            <id value="18965b02-b29f-42f4-9459-535deb2eaacc"/>
            <extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1" >
                <extension url="removalReason" >
                    <valueCodeableConcept>
                        <coding>
                            <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1"/>
                            <code value="Error"/>
                            <display value="The Reasonable Adjustment Flag was created in error"/>
                        </coding>
                    </valueCodeableConcept>
                </extension>
                <extension url="supportingComment" >
                    <valueString value="Reasonable Adjustment Flag was created in error" />
                </extension>
            </extension>
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
            <id value="db4e7f9f-6730-4d48-b372-de7e5bae8bd4"/>
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
            <reference value="urn:uuid:18965b02-b29f-42f4-9459-535deb2eaacc"/>
        </item>
    </entry>
    <entry>
        <deleted value="false"/>
        <date value="2023-04-11T11:00:00+00:00"/>
        <item>
            <reference value="urn:uuid:db4e7f9f-6730-4d48-b372-de7e5bae8bd4"/>
        </item>
    </entry>
</List>

```

##### Request body - json

```json


{
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
            "id": "18965b02-b29f-42f4-9459-535deb2eaacc",
            "extension":  [
                {
                    "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1",
                    "extension":  [
                        {
                            "url": "removalReason",
                            "valueCodeableConcept": {
                                "coding":  [
                                    {
                                        "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1",
                                        "code": "Error",
                                        "display": "The Reasonable Adjustment Flag was created in error"
                                    }
                                ]
                            }
                        },
                        {
                            "url": "supportingComment",
                            "valueString": "Reasonable Adjustment Flag was created in error"
                        }
                    ]
                }
            ],
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
            "id": "db4e7f9f-6730-4d48-b372-de7e5bae8bd4",
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
                "reference": "urn:uuid:18965b02-b29f-42f4-9459-535deb2eaacc"
            }
        },
        {
            "deleted": false,
            "date": "2023-04-11T11:00:00+00:00",
            "item": {
                "reference": "urn:uuid:db4e7f9f-6730-4d48-b372-de7e5bae8bd4"
            }
        }
    ]
}


```

##### Http response

```
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Last-Modified: 2018-07-25T11:00:00+00:00
ETag: W/"0e356a77-0544-42ef-90a4-229a1cbe06af”
Content-Type: application/fhir+xml
```

##### Response body - xml

```xml
<List xmlns="http://hl7.org/fhir">
    <id value="fd756ccc-e6d2-4e40-991d-b022abc20aa0"/>
    <meta>
        <versionId value="0e356a77-0544-42ef-90a4-229a1cbe06af"/>
        <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"/>
    </meta>
    <contained>
        <Condition xmlns="http://hl7.org/fhir">
            <id value="18965b02-b29f-42f4-9459-535deb2eaacc"/>
            <extension url="https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1" >
                <extension url="removalReason" >
                    <valueCodeableConcept>
                        <coding>
                            <system value="https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1"/>
                            <code value="Error"/>
                            <display value="The Reasonable Adjustment Flag was created in error"/>
                        </coding>
                    </valueCodeableConcept>
                </extension>
                <extension url="supportingComment" >
                    <valueString value="Reasonable Adjustment Flag was created in error" />
                </extension>
            </extension>
            <clinicalStatus value="inactive"/>
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
            <id value="db4e7f9f-6730-4d48-b372-de7e5bae8bd4"/>
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
    <contained>
        <Provenance>
            <id value="a77a657b-9883-4c0f-b141-3b511ff07754"/>
            <target>
                <reference value="#"/>
            </target>
            <recorded value="2023-04-14T11:00:00+00:00"/>
            <activity>
                    <system value="http://hl7.org/fhir/v3/DataOperation"/>
                    <code value="UPDATE"/>
                    <display value="revise"/>
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
        <deleted value="true"/>
        <date value="2023-04-11T11:00:00+00:00"/>
        <item>
            <reference value="urn:uuid:18965b02-b29f-42f4-9459-535deb2eaacc"/>
        </item>
    </entry>
    <entry>
        <deleted value="false"/>
        <date value="2023-04-11T11:00:00+00:00"/>
        <item>
            <reference value="urn:uuid:db4e7f9f-6730-4d48-b372-de7e5bae8bd4"/>
        </item>
    </entry>
    <entry>
        <deleted value="false"/>
        <date value="2023-04-11T11:00:00+00:00"/>
        <item>
            <reference value="urn:uuid:a77a657b-9883-4c0f-b141-3b511ff07754"/>
        </item>
    </entry>
</List>

```

##### Response body - json

```json


{
    "resourceType": "List",
    "id": "fd756ccc-e6d2-4e40-991d-b022abc20aa0",
    "meta": {
        "versionId": "0e356a77-0544-42ef-90a4-229a1cbe06af",
        "profile":  [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1"
        ]
    },
    "contained":  [
        {
            "resourceType": "Condition",
            "id": "18965b02-b29f-42f4-9459-535deb2eaacc",
            "extension":  [
                {
                    "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1",
                    "extension":  [
                        {
                            "url": "removalReason",
                            "valueCodeableConcept": {
                                "coding":  [
                                    {
                                        "system": "https://fhir.nhs.uk/STU3/CodeSystem/RARecord-RemovalReason-1",
                                        "code": "Error",
                                        "display": "The Reasonable Adjustment Flag was created in error"
                                    }
                                ]
                            }
                        },
                        {
                            "url": "supportingComment",
                            "valueString": "Reasonable Adjustment Flag was created in error"
                        }
                    ]
                }
            ],
            "clinicalStatus": "inactive",
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
            "id": "db4e7f9f-6730-4d48-b372-de7e5bae8bd4",
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
        },
        {
            "resourceType": "Provenance",
            "id": "a77a657b-9883-4c0f-b141-3b511ff07754",
            "target":  [
                {
                    "reference": "#"
                }
            ],
            "recorded": "2023-04-14T11:00:00+00:00",
            "activity": {
                "system": "http://hl7.org/fhir/v3/DataOperation",
                "code": "UPDATE",
                "display": "revise"
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
            "deleted": true,
            "date": "2023-04-11T11:00:00+00:00",
            "item": {
                "reference": "urn:uuid:18965b02-b29f-42f4-9459-535deb2eaacc"
            }
        },
        {
            "deleted": false,
            "date": "2023-04-11T11:00:00+00:00",
            "item": {
                "reference": "urn:uuid:db4e7f9f-6730-4d48-b372-de7e5bae8bd4"
            }
        },
        {
            "deleted": false,
            "date": "2023-04-11T11:00:00+00:00",
            "item": {
                "reference": "urn:uuid:a77a657b-9883-4c0f-b141-3b511ff07754"
            }
        }
    ]
}


```


