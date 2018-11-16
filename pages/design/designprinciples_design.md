---
title: API Design
keywords: development
tags: [development,fhir]
sidebar: overview_sidebar
permalink: designprinciples_design.html
summary: "High-level design of the FHIR&reg; Reasonable Adjustments API"
---

{% include custom/search.warnbanner.html %}

## FHIR&reg; Reasonable Adjustments API ##

<img src="images/HighLevelDesign.png"/>

## Design Decisions ##

### Initial Design ###

Reasonable Adjustments initial design followed the [architectural principles](/designprinciples_open_api_principles.html) outlined.
This was a simple ReSTful design, based on loosely coupled resources aligned with the units of exchange within the API Operations.
- Adjustments are modelled as Flag resources
- Impairments are modelled as Condition resources
- Consent is modelled as a Consent resource

As Adjustments and Impairments are optional, the presence, or not, of an active Consent resource for a given Patient can stand for presence or absence of the Reasonable Adjustment Flag.  

Details of the practitioner recording the Reasonable Adjustment information are required for all items.
- Practitioner details are modelled as Provenance resources
- As Provenance is only relevant in the context of the parent resource, the API design _contains_ the Provenance of the resource author or updater within the parent Flag, Condition or Consent resource

Standard Create, Read and Update operations are used to write, read and soft delete the Reasonable Adjustment resources.

### INTEROPen Curation ###

Reasonable Adjustments underwent INTEROPen curation in April 2018. The initial design used the .category element to identify resources that are part of a Reasonable Adjustment Flag.

Curation recommended use of a List resource to identify Conditions that are part of a Reasonable Adjustment Flag in order to:
- limit .category valueset to clinical categories, protecting against category proliferation
- conform to a pattern established in GPConnect and Transfer of Care programmes

Reasonable Adjustments API has incorporated the recommended changes.