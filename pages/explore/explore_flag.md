---
title: RARecord Profiles
keywords: usecase, profile
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: explore_flag.html
summary: Specification of the RARecord-Flag-1 resource. This resource records details of each Reasonable Adjustment identified, by or for a patient, within the FHIR&reg; Reasonable Adjustments API.
---
{% include custom/search.warnbanner.html %}

{% comment %}

    ** RARecord-Flag-1 **
    =====================

    {% endcomment %}

## Reasonable Adjustments - Adjustments ##

The Flag resource, profiled as RARecord-Flag-1, will record specific [Adjustments - as defined under the Equality Act (2010)](https://www.gov.uk/government/publications/reasonable-adjustments-a-legal-duty/reasonable-adjustments-a-legal-duty) - that are identified by the patient, or supporting healthcare professionals, to increase access to effective, informed and supportive health care.

{% include custom/fhir.resourcegrid.html
resourcename="RARecord-Flag-1"
resource="[RARecord-Flag-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Flag-1/_history/0.0.5)"
ccresource="Not Available"
fhirresource="[Flag](https://www.hl7.org/fhir/flag.html)" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/RARecord-Flag-1-example-1.xml"
title="RARecord-Flag-1"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/RARecord-Flag-1-example-1.json"
title="RARecord-Flag-1"
type="json" %}

---