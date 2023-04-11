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
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
```

##### Response body - xml

```
```

##### Response body - json

```
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
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
```

##### Response body - xml

```
```

##### Response body - json

```
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
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
```

##### Response body - xml

```
```

##### Response body - json

```
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
```

##### Request body - xml

```
```

##### Request body - json

```
```

##### Http response

```
```

##### Response body - xml

```
```

##### Response body - json

```
```

