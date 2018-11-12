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
resource="[RARecord-Provenance-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Provenance-1/_history/0.0.5)"
ccresource="Not Available"
fhirresource="[Provenance](https://www.hl7.org/fhir/provenance.html)" %}

Provenance is a contained resource in the Flag, Condition, Consent resources (and shows in the Contained section of the examples above).

### Design note: ###
Practitioner, Organisation and Role information can be identified by Referencing and can be accomplished within contained Provenance resources alone:
 
#### Provenance ####

* target - reference, points to containing resources
* recorded - instant, time of create|update
* agent
  * role - codeableConcept - currently this is bound to SecurityRoleType (Extensible) in base, _assume_ needs to use/include(only) CodeSystem-CareConnect-SDSJobRoleName-1
  * who - reference(Practitioner)
    * reference - URI string, points to a (not currently resolvable) SDS FHIR endpoint e.g. https://~spineservices.nhs.uk/STU3/sdsserver/Practioner/[UUID]
    * display - string, holds name of practitioner
  * onBehalfOf - reference(Organization)
    * reference - URI string, points to a ODS API endpoint e.g. https://directory.spineservices.nhs.uk/STU3/Organization/[OrgCode]
    * display - string, holds name of organization

Under this model, there's not going to be a contained Provenance resource on Create (or for an Update, no Extension.updated provenance). It's constructed and contained server-side as part of the Create operation. Extension-RARecord-Provenance-1 Extension.created 1..1 cardinality is therefore relaxed to 0..1 will constrain differently to ensure well-formed feels like a FHIRPath expression saying: if this has a temporaryId, created is empty; if this has a permanent Id created exists.

---