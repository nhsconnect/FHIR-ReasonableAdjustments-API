---
title: Patient Demographics
keywords: demographics
tags: [rest, fhir, demographics]
sidebar: overview_sidebar
permalink: design_demographics.html
summary: Details of the ways to obtain and verify an NHS number before calling the reasonable adjustments API
---
{% include custom/search.warnbanner.html %}

## Patient Demographic Tracing ##

As a pre-requisite for calling the Reasonable Adjustments API, client systems MUST have traced the patient on PDS to ensure they have the correct NHS number for the patient.

The [Spine Core API spec](https://developer.nhs.uk/apis/spine-core/pds_overview.html) outlines the approaches available for this demographic trace.

