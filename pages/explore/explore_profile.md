---
title: RARecord Profiles
keywords: usecase, profile
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: explore_profile.html
summary: This page describes Resource and Profile StructureDefinitions required to support data transmission within the FHIR&reg; Reasonable Adjustments API.
---
{% include custom/search.warnbanner.html %}

{% comment %}

    ** RARecord-Flag-1 Section **
    =============================

    {% endcomment %}

{% include custom/fhir.resourcegrid.html
resourcename="RARecord-Flag-1"
resource="[RARecord-Flag-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Flag-1)"
ccresource="N/A Yet"
fhirresource="[Flag](https://www.hl7.org/fhir/flag.html)" %}

<div id="ImageAsset"><img src="images/resourceImages/FlagResource.png" style="width:350px;"></div>
<div id="ImageAsset"><img src="images/resourceImages/FlagExtensions1.png" style="width:350px;"></div>
<div id="ImageAsset"><img src="images/resourceImages/FlagExtensions2.png" style="width:350px;"></div>

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/RARecord-Flag-1-example-1.xml"
title="RARecord-Flag-1"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/RARecord-Flag-1-example-1.json"
title="RARecord-Flag-1"
type="json" %}

{% comment %}

    ** RARecord-Consent-1 Section **
    ================================

    {% endcomment %}

{% include custom/fhir.resourcegrid.html
resourcename="RARecord-Consent-1"
resource="[RARecord-Consent-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Consent-1"
ccresource="N/A Yet"
fhirresource="[Consent](https://www.hl7.org/fhir/consent.html)" %}

<div id="ImageAsset"><img src="images/resourceImages/ConsentResource.png" style="width:350px;"></div>
<div id="ImageAsset"><img src="images/resourceImages/ConsentExtensions.png" style="width:350px;"></div>

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/RARecord-Consent-1-example-1.xml"
title="RARecord-Consent-1"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/RARecord-Consent-1-example-1.json"
title="RARecord-Consent-1"
type="json" %}

{% comment %}

    ** CareConnect-RARecord-Condition-1 Section **
    ==============================================

{% endcomment %}

{% include custom/fhir.resourcegrid.html
resourcename="CareConnect-RARecord-Condition-1"
resource="[CareConnect-RARecord-Condition-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-Condition-1)"
ccresource="[CareConnect-Condition-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Condition-1)"
fhirresource="[Condition](https://www.hl7.org/fhir/condition.html)" %}

<div id="ImageAsset"><img src="images/resourceImages/ConditionResource.png" style="width:350px;"></div>
<div id="ImageAsset"><img src="images/resourceImages/ConditionExtensions.png" style="width:350px;"></div>

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/CareConnect-RARecord-Condition-1-example1.xml"
title="CareConnect-RARecord-Condition-1"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/CareConnect-RARecord-Condition-1-example1.json"
title="CareConnect-RARecord-Condition-1"
type="json" %}

{% comment %}

    ** CareConnect-RARecord-List-1 Section **
    =========================================

{% endcomment %}

{% include custom/fhir.resourcegrid.html
resourcename="CareConnect-RARecord-List-1"
resource="[CareConnect-RARecord-List-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1)"
ccresource="[CareConnect-List-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-List-1)"
fhirresource="[List](https://www.hl7.org/fhir/list.html)" %}

<div id="ImageAsset"><img src="images/resourceImages/ListResource.png" style="width:350px;"></div>

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/CareConnect-RARecord-List-1-example.xml"
title="CareConnect-RARecord-List-1"
type="xml" %}

{% include custom/fhir.codegrid.html
relfilepath="resourceexamples/CareConnect-RARecord-List-1-example.json"
title="CareConnect-RARecord-List-1"
type="json" %}

{% comment %}

    ** RARecord-Provenance-1 Section **
    =========================================

{% endcomment %}

{% include custom/fhir.resourcegrid.html
resourcename="RARecord-Provenance-1"
resource="[RARecord-Flag-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Provenance-1)"
ccresource="N/A Yet"
fhirresource="[Provenance](https://www.hl7.org/fhir/provenance.html)" %}

<div id="ImageAsset"><img src="images/resourceImages/Provenance.png" style="width:350px;"></div>

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

