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
PUT https://clinicals.spineservices.nhs.uk/STU3/[EndpointName]/[id uuid] HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: [traceId uuid]
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:[EndpointName].write:1
If-Match: W/"[versionId uuid]"
```


##### Request body - xml

```xml
```

##### Request body - json

```json
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
```

##### Response body - json

```json
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
PUT https://clinicals.spineservices.nhs.uk/STU3/[EndpointName]/[id uuid] HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: [traceId uuid]
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:[EndpointName].write:1
If-Match: W/"[versionId uuid]"
```


##### Request body - xml

```xml
```

##### Request body - json

```json
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
```

##### Response body - json

```json
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
PUT https://clinicals.spineservices.nhs.uk/STU3/[EndpointName]/[id uuid] HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: [traceId uuid]
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:[EndpointName].write:1
If-Match: W/"[versionId uuid]"
```


##### Request body - xml

```xml
```

##### Request body - json

```json
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
```

##### Response body - json

```json
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
PUT https://clinicals.spineservices.nhs.uk/STU3/[EndpointName]/[id uuid] HTTP/1.1
Authorization: Bearer [jwt_token_string]
FromASID: 123456123456
ToASID: 987654456789
TraceID: [traceId uuid]
Content-Type: application/fhir+xml
Prefer: return=representation
InteractionID: urn:nhs:names:services:raflags:[EndpointName].write:1
If-Match: W/"[versionId uuid]"
```


##### Request body - xml

```xml
```

##### Request body - json

```json
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
```

##### Response body - json

```json
```


