---
title: RARecord Profiles
keywords: usecase, profile
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: explore_condition.html
summary: Specification of the CareConnect-RARecord-Condition-1 resource. This resource records details of Impairments, under the Equality Act 2010 definition, recorded by or for a Patient within the FHIR&reg; Reasonable Adjustments API.
---
{% include custom/search.warnbanner.html %}

{% comment %}

    ** CareConnect-RARecord-Condition-1 **
    ======================================

    {% endcomment %}

## Reasonable Adjustments - Impairments ##

The Condition resource, profiled as CareConnect-RARecord-Condition-1, will record specific [Impairments - as defined under the Equality Act (2010)](https://www.gov.uk/definition-of-disability-under-equality-act-2010) - that are identified by the patient, or supporting healthcare professionals, to increase access to effective, informed and supportive health care.

{% include custom/fhir.resourcegrid.html
resourcename="CareConnect-RARecord-Condition-1"
resource="[CareConnect-RARecord-Condition-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-Condition-1)"
ccresource="[CareConnect-Condition-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Condition-1)"
fhirresource="[Condition](https://www.hl7.org/fhir/condition.html)" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/CareConnect-RARecord-Condition-1-example1.xml"
title="CareConnect-RARecord-Condition-1"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/CareConnect-RARecord-Condition-1-example1.json"
title="CareConnect-RARecord-Condition-1"
type="json" %}

---