---
title: API Security
keywords: security
tags: [rest, fhir, security]
sidebar: overview_sidebar
permalink: design_security.html
summary: An overview of the security requirements for FHIR API calls into Spine.
---
{% include custom/search.warnbanner.html %}

## System Identifiers and Certificates ##

In order to be able to make API calls into Spine for the Reasonable Adjustments API in a live (or [path-to-live](https://developer.nhs.uk/apis/spine-core/test_environments.html)) Spine environment, clients first need to go through an assurance process with NHS Digital.

After completing this assurance process, the supplier of the calling system will be provided with a client certificate and an ASID (Accredited System ID) to use to secure access and identify the calling system in Spine calls. This must be used in all calls into the API - the overall process for identifying and securing calls from system endpoints is common for all Spine FHIR APIs, and is described in the [Spine Core API spec](https://developer.nhs.uk/apis/spine-core/build_endpoints_example_spine_fhir.html).

## User Identifiers and RBAC ##

All health and care professionals using systems that access Spine are required to use national identities, and adhere to national Role Based Access Controls (RBAC) to ensure patient data is only accessed by individuals in an appropriate role for the data being accessed.

Currently, this is controlled through the use of Smartcards and the Care Identity Service (CIS), although in future new NHS Identity services will provide other mechanisms for users to authenticate themselves for access to services. For the moment however, all clients MUST implement the CIS smartcard services, and apply appropriate RBAC controls before calling the Reasonable Adjustments API. There is an overview of how this can be done in the "legacy messaging" section of the [Spine Core API spec](https://developer.nhs.uk/apis/spine-core/smartcards.html)

## Passing System and User Context into API calls ##

To support audit and provenance within the Spine, the information about both the calling system and the authenticated user MUST be passed into the Reasonable Adjustment API calls in the form of an OAuth Access (bearer) token - specifically an encoded JSON web token.

In the future NHS Identity solution will provide an authorisation endpoint that can grant these tokens to authorised users/systems, but until that service is available the calling system must generate the token itself. The specification of this token, what should be in it, and how it can be generated can be found in the [Spine Core API spec](https://developer.nhs.uk/apis/spine-core/security_jwt.html).

