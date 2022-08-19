---
title: Headers
keywords: security
tags: [rest, fhir, security]
sidebar: overview_sidebar
permalink: design_headers.html
summary: An overview of the security requirements for FHIR API calls into Spine.
---
{% include custom/search.warnbanner.html %}

## Headers ##

This page collates and summarises http headers to be included with http requests and responses submitted.

It is recommended that developers are familiar with and refer to technical documentation [Introduction to Spine Core FHIR API Framework](https://developer.nhs.uk/apis/spine-core/index.html) while integrating with any Spine systems.

Headers listed are cumulative.
### Requests ###

#### All requests ####
* Authorization: Bearer [jwt_token_string]
* FromASID: [clientASID]
* ToASID: [serverASID]
* TraceID: [client ,message uuid]
* InteractionID: [serviceName]

[InteractionID](/design_headers.html#interactionid) varies by resource and interaction undertaken.

FromASID and ToASID headers, TraceID and Accredited System IDs are specified in the [Spine Core FHIR API Framework](
https://developer.nhs.uk/apis/spine-core/ssp_implementation_guide.html#system-responsibilities)

#### Create requests ####
* Prefer: return=representation

#### Update requests ####
* If-Match: [versionIdETag]
* Prefer: return=representation

### Responses ###

#### All Read & failure responses ####
* Date: [servedNowDate]
* Content-type: application/fhir+json or application/fhir+xml

#### All successful Create responses ####
* Date: [servedNowDate]
* Last-Modified: [lastModDate]
* Location: https://clinicals.spineservices.nhs.uk/STU3/[type]/[id]/_history/[vid]
* ETag: W/"[versionId]"
* Content-type: application/fhir+json or application/fhir+xml

#### All successful Update responses ####
* Date: [servedNowDate]
* Last-Modified: [lastModDate]
* ETag: W/"[versionId]"
* Content-type: application/fhir+json or application/fhir+xml


## InteractionID ##


<table>

    <thead>
        <tr>
            <th>Interaction</th>
            <th>Resource</th>
            <th>InteractionID</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="4">Read</td>
            <td>Consent</td>
            <td>urn:nhs:names:services:raflags:Consent.read:1</td>
        </tr>
        <tr>
            <td>Flag</td>
            <td>urn:nhs:names:services:raflags:Flag.read:1</td>
        </tr>
        <tr>
            <td>Condition</td>
            <td>urn:nhs:names:services:raflags:Condition.read:1</td>
        </tr>
        <tr>
            <td>List</td>
            <td>urn:nhs:names:services:raflags:List.read:1</td>
        </tr>
        <tr>
            <td rowspan="5">Create, Update,<br>Delete</td>
            <td>Consent</td>
            <td>urn:nhs:names:services:raflags:Consent.write:1</td>
        </tr>
        <tr>
            <td>Flag</td>
            <td>urn:nhs:names:services:raflags:Flag.write:1</td>
        </tr>
        <tr>
            <td>Condition</td>
            <td>urn:nhs:names:services:raflags:Condition.write:1</td>
        </tr>
        <tr>
            <td>List</td>
            <td>urn:nhs:names:services:raflags:List.write:1</td>
        </tr>
        <tr>
            <td>$removeflag</td>
            <td>urn:nhs:names:services:raflags:removeflag.write:1</td>
        </tr>
    </tbody>

</table>

