---
title: Read Use Cases
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_Read.html
summary: Read Use Cases describes the http request response behaviour of the endpoints and methods supported by the FHIR&reg; Reasonable Adjustments API to Read resources
---
{% include custom/search.warnbanner.html %}

## Read Use Cases

This page specifies the Read/GET use cases to be supported by the FHIR&reg; Reasonable Adjustments API.

### Consent

#### Summary:
Practitioner wishes to view/read Consent information in RA record


#### Main

* Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve Consent RARecord component
    * ClientSystem submits Read Consent request
      * ServerSystem submits Read Consent response

#### Examples

##### Http request

```
GET https://clinicals.spineservices.nhs.uk/STU3/Consent?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
TraceID: 2dc56572-e1c5-4f12-a53d-12a7b91669c8
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Consent.read:1
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Content-Type: application/fhir+xml
```

##### Response body - xml

```
```

##### Response body - json

```
```

### List

#### Summary:
Practitioner wishes to view/read Impairments information in RA record


#### Main

* Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve Impairments RARecord component
    * ClientSystem submits Read Impairment request
      * ServerSystem submits Read Impairment response

#### Examples

##### Http request

```
GET https://clinicals.spineservices.nhs.uk/STU3/List?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
TraceID: 4f4b65cc-2868-4956-b696-aef42cdc69e9
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:List.read:1
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Content-Type: application/fhir+xml
```


##### Response body - xml

```
```

##### Response body - json

```
```

### Flag

#### Summary:
Practitioner wishes to view/read Adjustments information in RA record


#### Main

* Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve Adjustment RARecord component
    * ClientSystem submits Read Adjustment request
      * ServerSystem submits Read Adjustment response

#### Examples

##### Http request

```
GET https://clinicals.spineservices.nhs.uk/STU3/Flag?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
TraceID: 91ed17a2-e866-480b-9583-eafc01fac418
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:Flag.read:1
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Content-Type: application/fhir+xml
```


##### Response body - xml

```
```

##### Response body - json

```
```

### UnderlyingConditions

#### Summary:
Practitioner wishes to view/read Underlying Condition information in RA record


#### Main

* Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve Underlying Conditions RARecord component
    * ClientSystem submits Read Underlying Condition request
      * ServerSystem submits Read Underlying Condition response

#### Examples

##### Http request

```
GET https://clinicals.spineservices.nhs.uk/STU3/UnderlyingConditions?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
TraceID: 7c438c87-34f5-42e1-8a7d-c7deccfac9be
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:UnderlyingConditions.read:1
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Content-Type: application/fhir+xml
```


##### Response body - xml

```
```

##### Response body - json

```
```

### ThresholdCode

#### Summary:
Practitioner wishes to view/read Threshold Code information in RA record


#### Main

* Practitioner retrieves Patient's RARecord.  
  * ClientSystem queries ServerSystem to retrieve Threshold Code RARecord component
    * ClientSystem submits Read Threshold Code request
      * ServerSystem submits Read Threshold Code response

#### Examples

##### Http request

```
GET https://clinicals.spineservices.nhs.uk/STU3/ThresholdCode?
 patient=999999998&
 status=active&
 category=https://fhir.nhs.uk/STU3/CodeSystem/CodeSystem-RARecord-FlagCategory-1|reasonable%20adjustments%20flag&
 _format=xml HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 654321123456
ToASID: 987654456789
TraceID: 2a75c016-2f7e-4444-81c0-cae8ca208796
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:ThresholdCode.read:1
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
HTTP/1.1 200 OK
Date: Tue, 11 Apr 2023 11:00:00 GMT
Content-Type: application/fhir+xml
```


##### Response body - xml

```
```

##### Response body - json

```
```


