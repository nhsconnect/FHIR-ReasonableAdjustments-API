---
title: Identifiers
keywords: identifiers
tags: [rest, fhir]
sidebar: overview_sidebar
permalink: design_identifiers.html.html
summary: A note on the use of Identifiers in FHIR examples
---
{% include custom/search.warnbanner.html %}

## Identifiers ##

Examples in this specification use illustrative identifiers for elements such as:
``` xml
    <whoReference>
        <reference value="https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9"/>
        <display value="Dr.D"/>
    </whoReference>
```
``` json
"whoReference": {
    "reference": "https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9",
    "display": "Dr.D"
  },
```
or
``` xml
    <patient>
        <reference value="demographics.spineservices.nhs.uk/STU3/Patient/999999998"/>
    </patient>
```
``` json
"patient": {
    "reference": "demographics.spineservices.nhs.uk/STU3/Patient/999999998"
  },
```
These are [Identifiers](http://hl7.org/fhir/r4/datatypes.html#identifier), as per [rfc3986](https://tools.ietf.org/html/rfc3986). Their purpose is to uniquely identify a resource within a namespace. 

Use of a scheme within the URI (e.g. https) does not currently imply a resolvable endpoint. i.e. `GET https://sds.spineservices.nhs.uk/STU3/Practitioner/2ee4tr6a9` won't return a Practitioner resource. This position will change as work to make national data registers available progresses.
