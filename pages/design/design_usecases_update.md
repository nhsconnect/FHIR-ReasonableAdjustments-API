---
title: Interaction | Update
keywords: usecase
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_update.html
summary: Create operation describes interaction required to record a new Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 3 Update RA line ##


Trigger: Post-op appt with GP. Patient requests change RA Easy Read to Large Print

Pre-requisites:
Practioner Dr D. logged on w SmartCard/National Identity > URPId (PractitionerRole reference)
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB demographic data

System Scope: GPSystem client, Spine, PDS, SDS, RARecordSystem

Summary: During appt GP discusses RA Record. Patient requests change RA Easy Read to Large Print

* Pre
Patient arrives at post-op appt
Practitioner opens GPSystem, traces & verifies demographic info (internal call to PDS)
Practitioner opens Patient's RARecord
  System retrieves and displays RARecord for Patient's NHS#
* Main
Practitioner discusses RARecord and RA with Patient, Patient doesn't like Easy Read
Practitioner discusses options w Patient, Patient agrees change RA 'Easy Read' to 'Large Print'
  Practitioner opens RARecord line for RA 'Easy Read'
  Practitioner changes RA 'Easy Read' to 'Large Print'
    System presents RA Code valueset (CodeSystem-RARecord-ConditionCode-1), Practitioner selects
    System records RA details (e.g. 'Communication needs', 'Easy Read')
    System populates RARecord line Updater with Practitioner reference
Patient declines to record any more RAs
  Practitioner commits RARecord (or RARecord line)
    System does...
