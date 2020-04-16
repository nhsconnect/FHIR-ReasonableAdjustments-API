---
title: RARecord Profiles
keywords: usecase, profile
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: explore_consent.html
summary: Specification of the RARecord-Consent-1 resource. This resource records the consent to record and use Reasonable Adjustments information using the FHIR&reg; Reasonable Adjustments API.
---
{% include custom/search.warnbanner.html %}

{% comment %}

    ** RARecord-Consent-1 **
    ========================

    {% endcomment %}

    
## Reasonable Adjustments - Consent ##

The Consent resource, profiled as [RARecord-Consent-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Consent-1), records consent by a patient to record Reasonable Adjustment [Impairment](https://www.gov.uk/definition-of-disability-under-equality-act-2010) and [Adjustment](https://www.gov.uk/government/publications/reasonable-adjustments-a-legal-duty/reasonable-adjustments-a-legal-duty) information.  
This information will be available to healthcare professionals and organisations providing direct care to the patient, and to screening services, to ensure that key Adjustment information (such as communication requirements) is shared consistently across the NHS.  

{% include custom/fhir.resourcegrid.html
resourcename="RARecord-Consent-1"
resource="[RARecord-Consent-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Consent-1/_history/0.0.5)"
ccresource="Not Available"
fhirresource="[Consent](https://www.hl7.org/fhir/consent.html)" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/RARecord-Consent-1-example-1.xml"
title="RARecord-Consent-1"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/RARecord-Consent-1-example-1.json"
title="RARecord-Consent-1"
type="json" %}

---