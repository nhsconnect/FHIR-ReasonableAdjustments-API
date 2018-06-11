---
title: Interaction | Add
keywords: usecase
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_add.html
summary: Create operation describes interaction required to add a new Adjustment to a Reasonable Adjustment Flag on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 2 Add RA line ##

Trigger: Mrs M has referral to inpatient procedure. RA Flag triggers pre-op appt with Learning Disability Nurse N. Nurse N discusses Mrs M's situation and records a new, appropriate RA.

Pre-requisites:
Practioner Nrs N. logged on w SmartCard/National Identity > URPId (PractitionerRole reference)
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB demographic data

System Scope: Acute/DepartmentalSystem? client, Spine, PDS, SDS, RARecordSystem

Summary: Patient discusses RA need re reading difficulties; requests record RA Easy Read

* Pre
Patient arrives at pre-op appt
Practitioner opens AcuteSystem, traces & verifies demographic info (internal call to PDS)
Practitioner opens Patient's RARecord
  System retrieves and displays RARecord for Patient's NHS#
* Main
Practitioner discusses RARecord with Patient
Patient states has difficulty reading
(Practitioner opens, views RA Category
  System displays RA Category picklist (CodeSystem-RARecord-CarePlanActivityCategory-1)
  Practitioner selects code Communication needs
  System displays RA Code picklist (CodeSystem-RARecord-CarePlanActivity-1))
Practitioner discusses options w Patient, Patient agrees RA 'Easy Read'
  Practitioner creates new RARecord line for RARecord
    System populates RARecord with RARecord line ref (logical Id?) (or System populates RARecord line with RARecord ref depending on direction)
    System populates RARecord line Creator with Practitioner reference
  Practitioner adds RA from coded picklist
    System presents RA Category valueset (CodeSystem-RARecord-ConditionCode-1), Practitioner selects
    System presents RA Code valueset (CodeSystem-RARecord-ConditionCode-1), Practitioner selects
    System records RA details (e.g. 'Communication needs', 'Easy Read')
Patient declines to record any more RAs
  Practitioner commits RARecord
    System does...