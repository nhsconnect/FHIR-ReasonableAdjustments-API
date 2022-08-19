---
title: RARecord Profiles
keywords: usecase, profile
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: explore_provenance.html
summary: This page describes the RARecord-Provenance-1 resource. This holds details of the user recording information within the FHIR&reg; Reasonable Adjustments API.
---
{% include custom/search.warnbanner.html %}

{% comment %}

    ** RARecord-Provenance-1 **
    ===========================

{% endcomment %}

## Reasonable Adjustments - Provenance ##

The Provenance resource, profiled as RARecord-Provenance-1, records details of the healthcare professional recording the Reasonable Adjustment information, for audit and clinical attestation purposes.  

{% include custom/fhir.resourcegrid.html
resourcename="RARecord-Provenance-1"
resource="[RARecord-Provenance-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Provenance-1)"
ccresource="Not Available"
fhirresource="[Provenance](https://www.hl7.org/fhir/provenance.html)" %}

Provenance is a contained resource in the Flag and Consent resources (and shows in the Contained section of the examples above). For these resources, Provenance is constructed and populated server-side.

For Condition resources, the Provenance resource is constructed by the client. It is contained within the List resource, alongside the Condition resources (rather than contained in).


#### Provenance ####

| target | reference | points to resource for which it captures Provenance |
| recorded | instant | time of create\|update |
| agent.role | codeableConcept | role SHOULD use a value from [ValueSet-RARecord-ProvenanceRole-1](https://fhir.nhs.uk/STU3/ValueSet/ValueSet-RARecord-ProvenanceRole-1) |
| agent.who | reference(Practitioner) |
| agent.who.reference | URI | points to a (not currently resolvable) SDS FHIR endpoint e.g. https://~spineservices.nhs.uk/STU3/sdsserver/Practioner/[UUID] |
| agent.who.display | string | holds name of practitioner |
| agent.onBehalfOf | reference(Organization) |
| agent.onBehalfOf.reference | URI | points to a ODS API endpoint e.g. https://directory.spineservices.nhs.uk/STU3/Organization/[OrgCode] |
| agent.onBehalfOf.display | string | holds name of organization |

Under this model, there's not going to be a contained Provenance resource on Create of Flag or Consent resources (or for an Update, no Extension.updated provenance), as it's constructed and contained server-side as part of the persist operation. Extension-RARecord-Provenance-1 Extension.created 1..1 cardinality has therefore relaxed to 0..1.

---