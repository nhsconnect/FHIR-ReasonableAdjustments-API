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
- Equality Act Threshold, Impairments and Underlying Conditions are modelled as Condition resources
- Consent is modelled as a Consent resource

#### Consent

As Adjustments and Impairments are optional, the presence, or not, of an active Consent resource for a given Patient can stand for presence or absence of the Reasonable Adjustment Flag.  

#### Adjustments

Adjustments are used to represent individual Adjustments.
- Adjustments SHOULD be recorded in .code as a code selected from the SNOMED CT valueset RARecord-FlagCode-1

#### Equality Act Threshold, Impairments and Underlying Conditions

Condition resources are used to represent 3 related entities within the Reasonable Adjustment Flag record:

Equality Act Threshold
- A Reasonable Adjustment Flag record SHALL contain a Condition recording that the patient meets the Equality Act Threshold. 
- This SHALL be recorded as a Condition resource with .code set to SNOMED CT concept 1326341000000105 \| Impairment with substantial and long term adverse effect on normal day to day activity (Equality Act 2010)


Impairments
-  A Reasonable Adjustment Flag record MAY (optionally) contain further Condition resources detailing additional Impairments details
- These SHALL be recorded as Condition resources with .code set to a code value from CodeSystem CodeSystem -RARecord-ConditionCode-1
    
Underlying Conditions
- A Reasonable Adjustment Flag record MAY (optionally) also contain further Condition resources detailing Underlying Conditions that are relevant to provision of reasonable adjustments to care
- These SHALL be recorded as Condition resources with .code set to the relevant SNOMED CT concept

#### Provenance

Details of the practitioner recording the Reasonable Adjustment information are required for all items.
- Practitioner details are modelled as Provenance resources
- As Provenance is only relevant in the context of the parent resource, the API design _contains_ the Provenance of the resource author or updater within the parent Flag, Condition or Consent resource

Standard Create, Read and Update operations are used to write, read and soft delete the Reasonable Adjustment resources.

### INTEROPen Curation ###

Reasonable Adjustments underwent INTEROPen curation in April 2018. The initial design used the .category element to identify resources that are part of a Reasonable Adjustment Flag.

Curation recommended use of a List resource to identify Conditions that are part of a Reasonable Adjustment Flag in order to:
- limit .category valueset to clinical categories, protecting against category proliferation
- conform to a pattern established in GPConnect and Transfer of Care programmes

Further design constraints recommended an approach where Reasonable Adjustment Condition resources are exchanged as a unit, by containing the Conditions as elements withina single List per patient. This List to be managed client-side, and to contain the relevant Provenance information.

Reasonable Adjustments API has incorporated the recommended changes.