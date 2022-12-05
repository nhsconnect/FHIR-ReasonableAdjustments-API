---
title: Release Notes
keywords: development, versioning
tags: [development]
sidebar: overview_sidebar
permalink: overview_release_notes.html
summary: Summary release notes of the FHIR&reg; Reasonable Adjustments API Implementation Guide
---

{% include important.html content="This site is under active development by NHS Digital and is intended to provide all the technical resources you need to successfully develop applications using the FHIR&reg; Reasonable Adjustments API. This project is being developed using an agile methodology so iterative updates to content will be added on a regular basis." %}

## 0.3.5-beta

### Updated Technical assets

Terminology
- valuesets and codesystems updated in line with new valuesets in Reasonable Adjustment Flag
Local System Integration Requirements Specification v1.1
- 'PRECONDITION_FAILED' added to Spine-ErrorOrWarningCode-1

Profiles
- profiles for Consent, Flag, Condition - removed circular extension Extension-RARecord-Provenance-1
- profile Provenance .activity now 1..1 

Technical asset changes can be viewed via the relevant git compare page in the [Github repo](https://github.com/nhsconnect/STU3-FHIR-Assets/compare/2bfbb694...develop)

### Update Implementation Guide

- Terminology page describing usage added
- Design principles expanded to clarify Resource usage. Introduces Equality Act Threshold, Impairments and Underlying Conditions distinction for Conditions.
- TraceId and clearer call out to Spine added to Headers page

## 0.3.4-beta

- clarification of requirement that supporting comments are mandatory when removing an RA Flag or a constituent resource
- update of Extension-RARecord-RemovalReason-1 to carry supporting comment
- update of OperationDefinition RARecord-RemoveRARecord-Operation-1 to pass supporting comment as in-parameter
- update of Interactions, Use Cases and examples to conform

## 0.3.3-beta

- uplift of examples to reference updated valuesets and codesystems
- [diff vs. 0.3.2-beta](https://github.com/nhsconnect/FHIR-ReasonableAdjustments-API/compare/4d40e7462e2a72bdcf2198166d3d1dc1b4835c50..b38d3b844d7df34a9d5be005bb5fabb103ff619e)

## 0.3.2-beta 

- correction of List-Condition design
- [diff vs. 0.3.1-beta](https://github.com/nhsconnect/FHIR-ReasonableAdjustments-API/compare/a533284c515d0383aa49b1422319229b0d04776d..4d40e7462e2a72bdcf2198166d3d1dc1b4835c50)

## 0.3.1-beta

- corrections to examples

## 0.3.0-beta

- update IG in line with design decision to use List-Condition structure for Reasonable Adjustment conditions


## 0.2.0-beta

- reorder of pages

## 0.1.0-alpha ##

- clarification of headers and jwt payload
- clarification of profile metadata in examples
- rewrite and reordering of use cases and examples  
  (to clarify and to reflect the above)
- No RA Record updated examples to show empty bundle response
- Create Interaction 1 Consent per NHS Number business rule added
- removeflag operation renamed as removerarecord
- Remove RA Record use cases and examples aligned with rename
- Removal of Consent triggers Remove RA Record operation noted on Remove RA Record interaction page, use case page
- Refreshed Read an RA Record and Add Adjustmen, Add Impairment Response JSON examples to align with XML examples

## 0.0.5-alpha ##

- updates and clarifications from DDC Spine Core design review

## 0.0.4-alpha ##

- Updates to cover resource versioning, caching and managing conflicting updates
- Added Design section with information about tracing patients and API security
- Additional examples covering multi-resource searchset bundle Read example, Adjustments (Flag resources) with coded data, unstructured (freetext) data, and with both.
- Corrected Flag Server endpoint to https://clinicals.spineservices.nhs.uk/STU3 

## 0.0.3-alpha ##

- Design updates covering operations to support Provenance and Remove Flag functionality

## 0.0.2-alpha ##

- Incremental release with coverage of Interaction use cases and examples

## 0.0.1-alpha ##

- Initialization of the FHIR&reg; Reasonable Adjustments API implementation guide.
