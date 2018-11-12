---
title: RARecord Profiles
keywords: usecase, profile
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: explore_list.html
summary: This page describes the CareConnect-RARecord-List-1 resource. This organises and identifies CareConnect-RARecord-Condition-1 resources recording Impairments within the FHIR&reg; Reasonable Adjustments API.
---
{% include custom/search.warnbanner.html %}

{% comment %}

    ** CareConnect-RARecord-List-1 **
    =================================

    {% endcomment %}

## Reasonable Adjustments - List ##

The List resource, profiled as CareConnect-RARecord-List-1, is used to identify Impairment Condition resources for a particular patient.  
This maintains a pattern for referencing Condition resources established in GPConnect and Transfer of Care programmes.

{% include custom/fhir.resourcegrid.html
resourcename="CareConnect-RARecord-List-1"
resource="[CareConnect-RARecord-List-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-RARecord-List-1/_history/0.0.5)"
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

---