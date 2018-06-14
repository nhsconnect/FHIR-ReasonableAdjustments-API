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

{% include custom/fhir.resourcegrid.html
resourcename="RARecord-Provenance-1"
resource="[RARecord-Flag-1](https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Provenance-1)"
ccresource="N/A Yet"
fhirresource="[Provenance](https://www.hl7.org/fhir/provenance.html)" %}

Placeholder text: Provenance is a contained resource in Flag, Condition, Consent resources (and shows in the Contained section of the examples).
Provenance has been reconsidered during detailed design work, and will be modified in v0.0.3

{% comment %}

    ** Graveyard Section **
    =======================

{% endcomment %

Placeholder text: PractitionerRole, Practitioner and Organization are no longer required, following detailed design on Provenance solution. No examples have been added in v0.0.2 and the profiles will be removed from v0.0.3

{% include custom/fhir.resourcegrid.html
resourcename="CareConnect-RARecord-PractitionerRole-1"
resource="[CareConnect-RARecord-PractitionerRole-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-PractitionerRole-1)"
ccresource="[CareConnect-PractitionerRole-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-PractitionerRole-1)"
fhirresource="[PractitionerRole](https://www.hl7.org/fhir/practitionerrole.html)" %}

{% include custom/fhir.resourcegrid.html
resourcename="CareConnect-RARecord-Organization-1"
resource="[CareConnect-RARecord-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-Organization-1)"
ccresource="[CareConnect-Organization-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Organization-1)"
fhirresource="[Organization](https://www.hl7.org/fhir/organization.html)" %}

{% include custom/fhir.resourcegrid.html
resourcename="CareConnect-RARecord-Practitioner-1"
resource="[CareConnect-RARecord-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-Practitioner-1)"
ccresource="[CareConnect-Practitioner-1](https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Practitioner-1)"
fhirresource="[Practitioner](https://www.hl7.org/fhir/practitioner.html)" %}





