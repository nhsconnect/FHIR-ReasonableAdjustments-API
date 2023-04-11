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
  * Practitioner records Consent removal
    * ClientSystem captures and structures Consent removal information
* Practitioner commits RARecord
    * ClientSystem submits Remove Consent request
      * ServerSystem submits Remove Consent response

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
Patient wishes to remove Adjustment. Practitioner records Adjustment removed


#### Main

* Patient wishes to remove an Adjustment
  * Practitioner records Adjustment removal
    * ClientSystem captures and structures Adjustment removal information
* Practitioner commits RARecord
    * ClientSystem submits Remove Adjustment request
      * ServerSystem submits Remove Adjustment response

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
Patient wishes to remove Impairment. Practitioner records Impairment removed


#### Main

* Patient wishes to remove an Impairment
  * Practitioner records Impairment removal
    * ClientSystem captures and structures Impairment removal information
* Practitioner commits RARecord
    * ClientSystem submits Remove Impairment request
      * ServerSystem submits Remove Impairment response

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
Patient wishes to remove Underlying Condition. Practitioner records Underlying Condition removed


#### Main

* Patient wishes to remove an Underlying Condition
  * Practitioner records Underlying Condition removal
    * ClientSystem captures and structures Underlying Condition removal information as new RARecord Condition-1 resource
* Practitioner commits RARecord
    * ClientSystem submits Remove Underlying Condition request
      * ServerSystem submits Remove Underlying Condition response

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


