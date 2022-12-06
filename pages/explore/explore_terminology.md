---
title: RARecord Terminology
keywords: usecase, profile
tags: [rest, fhir, development]
sidebar: accessrecord_rest_sidebar
permalink: explore_terminology.html
summary: Specification of Terminology usage within the FHIR&reg; Reasonable Adjustments API.
---
{% include custom/search.warnbanner.html %}

Resource profiles and extensions used in Reasonable Adjustments use the following terminology resources

### Profiles

- [RARecord-Consent-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Consent-1)
        
Consent.category (Example) uses [ValueSet/RARecord-FlagCategory-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-FlagCategory-1)

-- Identifies the Consent resource instance as being categorised as part of a Reasonable Adjustment Flag

Consent.purpose (Extensible) uses [ValueSet/RARecord-ConsentPurpose-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-ConsentPurpose-1)

-- Identifies the purpose of use (scope) controlled by this consent resource instance are for consent to record and share Reasonable Adjustments for provision of direct health care

- [RARecord-Flag-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Flag-1)
        
Flag.category (Required) uses [ValueSet/RARecord-FlagCategory-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-FlagCategory-1)

-- Identifies the Flag resource instance as being categorised as part of a Reasonable Adjustment Flag
    
Flag.code (Extensible) uses [ValueSet/RARecord-FlagCode-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-FlagCode-1)

-- Identifies the Reasonable Adjustment required

- [CareConnect-RARecord-Condition-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-Condition-1)
        
Condition.category (Required) uses [ValueSet/CareConnect-ConditionCategory-1](https://fhir.hl7.org.uk/STU3/ValueSet/CareConnect-ConditionCategory-1)

-- Identifies the Condition is catgeorised as an issue

Condition.code (Preferred) uses [ValueSet/RARecord-ConditionCode-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-ConditionCode-1)

-- Identifies the Condition (optionally) recorded for which the Reasonable Adjustment is applied. The broad Condition categories enumerated in https://fhir.nhs.uk/STU3/CodeSystem/RARecord-ConditionCode-1 are preferred, but specific coding, e.g. from SNOMED CT, may be used if desired.

- [CareConnect-RARecord-List-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1)

List.code (Required) uses [ValueSet/CareConnect-ListCode-1](https://fhir.nhs.uk/STU3/ValueSet/CareConnect-ListCode-1)

-- Identifies the type of the List resource instance. Use of '1094391000000102 \| Reasonable adjustments for health and care access' states the List is part of a Reasonable Adjustment Flag.

- [RARecord-Provenance-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Provenance-1)

Provenance.agent.role (Extensible) uses [ValueSet/RARecord-ProvenanceRole-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-ProvenanceRole-1)

-- Identifies the role of the agent, i.e. Practitioner, recording the Reasonable Adjustment Flag item.

### Extensions

- [Extension-RARecord-ProxyRole-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-ProxyRole-1)

.extension(consentingProxyRole) (Required) uses [ValueSet/RARecord-ProxyRole-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-ProxyRole-1)

-- Identifies the role type of a proxy recording consent for a Reasonable Adjustment Flag

- [Extension-RARecord-RemovalReason-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-RemovalReason-1)

.extension(removalReason) (Required) uses [ValueSet/RARecord-RemovalReason-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-RemovalReason-1)

-- Records the coded reason for removal of a Reasonable Adjustment Flag item

- [Extension-RARecord-AdjustmentCategory-1](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-RARecord-AdjustmentCategory-1)

.extension(adjustmentCategory) (Required) uses [ValueSet/RARecord-AdjustmentCategory-1](https://fhir.nhs.uk/STU3/ValueSet/RARecord-AdjustmentCategory-1)

-- Identifies the category of the Adjustment recorded.

