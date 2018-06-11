---
title: Interaction | Create
keywords: usecase
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_create.html
summary: Create operation describes interaction required to record a new Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Create RARecord ##


Trigger: GP initiate Reasonable Adjustment Flag discussion at annual health check

Pre-requisites:
Practioner Dr D. logged on w SmartCard/National Identity giving URPId (for PractitionerRole reference)
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB, demographic data
ClientSystem searched and failed to find existing RARecord

System Scope:
    ClientSystem includes GPSystem client, SCRa, 1-click etc.
    ServerSystem includes Spine, PDS, SDS, FlagServer etc.

Summary: Patient consents to record RA Flag; agrees to record LD as Impairment; declines to record any specific RAs

* Pre
Patient arrives at check
Practitioner opens GPSystem, traces & verifies demographic info (internal call to PDS)
Practitioner discusses RARecord with Patient
* Main
Patient consents to record RA Flag;
  Practitioner creates new RARecord for Patient (by recording Consent)
    System populates RARecord with Patient demographics
    System populates RARecord with Practitioner reference
  Practitioner records Patient consented to record RA info
    System populates RARecord with Consent details
Patient agrees to record LD as Reason;
  Practitioner adds Impairment from coded picklist (optionally elaborates w separate freetext)
    System presents valueset (CodeSystem-RARecord-ConditionCode-1)
    System records Impairment details (i.e. 'Learning Disability')
Patient declines to record any specific RAs
  Practitioner commits RARecord