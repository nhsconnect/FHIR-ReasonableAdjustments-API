---
title: JWT Payload and Scope
keywords: security
tags: [rest, fhir, security]
sidebar: overview_sidebar
permalink: design_jwt.html
summary: An overview of the specific security requirements for FHIR API calls into the FHIR&reg; Reasonable Adjustments API via Spine.
---
{% include custom/search.warnbanner.html %}


## Passing System and User Context into FHIR&reg; Reasonable Adjustments API calls ##

To support audit and provenance within the Spine, the information about both the calling system and the authenticated user MUST be passed into the Reasonable Adjustment API calls in the form of an OAuth Access (bearer) token - specifically an encoded JSON web token.

The general specification of this token, what should be in it, and how it can be generated can be found in the [Spine Core API spec](https://developer.nhs.uk/apis/spine-core/security_jwt.html).


### JWT Payload for RAFlag ###

Within this security framework, FHIR&reg; Reasonable Adjustments API calls should construct their Authorization Bearer tokens using:  

|Claim               |Mandatory     |Description                       |Fixed Value     |Dynamic Value           |Value                                   |DataType         |
|--------------------|--------------|----------------------------------|----------------|------------------------|----------------------------------------|-----------------|
|iss                 |Y             |issuer                            |No              |Yes                     |[Requesting systems issuer URI]         |URI              |
|sub                 |Y             |subject                           |No              |Yes                     |[User Identifier<br>URPId]                |Id               |
|aud                 |Y             |API endpoint URL                  |No              |Yes                     |[API endpoint URL]                      |URI <br> i.e. URI w/o query string|
|exp                 |Y             |expires                           |No              |Yes                     |[now + 5 minutes]                       |UTC Date         |
|iat                 |Y             |issued at                         |No              |Yes                     |[now]                                   |UTC Date         |
|reason_for_request  |Y             |purpose                           |directcare      |No                      |directcare                              |string           |
|scope               |Y             |Data requested                    |No              |Yes                     |[byInteraction] <br> see JWT scope      |string           |
|requesting_system             |Y             |Identifier for the system or device making the request      |No              |Yes                     |[System or Device Identifier]    |string           |
|requesting_organization       |Y             |Organisation making the request                             |No              |Yes                     |[Organisation Identifier]        |string           |
|requesting_user               |Y             |Health or Social Care professional making the request       |No              |Yes                     |[User Identifier<br>URPId]       |string           |

### JWT Scope ###

FHIR&reg; Reasonable Adjustments API Authorization Bearer tokens use SMART on FHIR scopes to control resource access and permissions.  
The scope required in the JWT Payload varies by Interaction:  

|Interaction     |Scope                  |
|----------------|-----------------------|
|Create Consent  |     user/Consent.write|
|Create Flag     |        user/Flag.write|
|Create Condition|   user/Condition.write|
|Create List     |        user/List.write|
|Read Consent    |      user/Consent.read|
|Read Adjustments|         user/Flag.read|
|Read Conditions |         user/Condition|
|Read List       |         user/List.read|
|Update List     |        user/List.write|
|Delete Consent  |     user/Consent.write|
|Delete Flag     |        user/Flag.write|
|Delete Condition|   user/Condition.write|
|Delete List     |        user/List.write|

### An example JWT payload for a Read Adjustments interaction ###
```
  {
    "iss": "https://scra.nhs.uk",
    "sub": "https://fhir.nhs.uk/Id/sds-role-profile-id|[SDSRoleProfileID]",
    "aud": "https://clinicals.spineservices.nhs.uk/STU3/F1ag",
    "exp": 1469496987,
    "iat": 1469436687,
    "reason_for_request": "directcare",
    "scope": "user/Flag.read"
  }
```
