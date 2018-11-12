---
title: API design principles
keywords: development
tags: [development,fhir]
sidebar: overview_sidebar
toc: false
permalink: designprinciples_open_api_principles.html
summary: "High-level design principles related to the API design"
---

{% include custom/search.warnbanner.html %}

## Open API

Reasonable Adjustments has aligned with [NHS England's Open API Policy](open-api-policy.pdf) to support the ambition of moving to a position where significant business functionality, available within systems, is exposed through interfaces where the definition is open.

## Architectural design principals

NHS Digital has a number of architectural design principles, some of which have developed based on interaction with the suppliers, others are based on an understanding of the technological maturity of the NHS at the present time and the other principals are based on good practice and a vision for the future of the NHS.


## Core API design principles

### FHIR

Reasonable Adjustments has adopted the [FHIR&reg; standard (STU3)](https://www.hl7.org/fhir/STU3/) and as such the FHIR API design principles will be followed unless a clear rationale exists to amend, in which case any deviation will be logged and the rationale clearly communicated.

Examples of FHIR principles that Reasonable Adjustments follows are:
- [FHIR RESTful API](https://www.hl7.org/fhir/STU3/http.html){:target="_blank"} principles will be used by default as this is the preferred approach by NHS Digital.
  - Synchronous endpoints using `GET`, `POST` and `PUT` HTTP verbs
- [FHIR operation](https://www.hl7.org/fhir/STU3/operations.html){:target="_blank"} APIs to be used in limited 'set piece' circumstances - for example, to pull bundles of resources without using the full generic querying syntax
- Business identifiers (such as NHS number) used to resolve a resource's [logical identity](https://www.hl7.org/fhir/STU3/resource.html#id){:target="_blank"}
- Resources represented as either [XML or JSON](https://www.hl7.org/fhir/STU3/formats.html#wire){:target="_blank"} as requested by the API consumer.  To ensure maximum accessibility, Reasonable Adjustments is expecting producers to support both formats.  However, since XML is on average 30% larger on the wire there is a preference towards use of JSON. 
- ETags for [managing version-aware updates](https://www.hl7.org/fhir/STU3/http.html#concurrency){:target="_blank"}


### Care Connect

GP Connect has worked to align as closely as possible with the Care Connect API, with an aim to maintain a wider interoperability. 
