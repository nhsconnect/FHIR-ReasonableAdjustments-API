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
Headers listed are cumulative.
### Requests ###

#### All requests ####
* Authorization: Bearer [jwt_token_string]
* FromASID: [clientASID]
* ToASID: [serverASID]
* InteractionID: [serviceName]

[InteractionID](/design_headers.html#interactionid) varies by resource and interaction undertaken.  
FromASID and ToASID headers, and Accredited System IDs are specified in the [Spine Core FHIR API Framework](https://developer.nhs.uk/apis/spine-core/resources_headers.html#other-headers)  

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
            <td>urn:nhs:names:services:flagserver:consent:read</td>
        </tr>
        <tr>
            <td>Flag</td>
            <td>urn:nhs:names:services:flagserver:flag:read</td>
        </tr>
        <tr>
            <td>Condition</td>
            <td>urn:nhs:names:services:flagserver:condition:read</td>
        </tr>
        <tr>
            <td>List</td>
            <td>urn:nhs:names:services:flagserver:list:read</td>
        </tr>
        <tr>
            <td rowspan="4">Create, Update,<br>Delete</td>
            <td>Consent</td>
            <td>urn:nhs:names:services:flagserver:consent:write</td>
        </tr>
        <tr>
            <td>Flag</td>
            <td>urn:nhs:names:services:flagserver:flag:write</td>
        </tr>
        <tr>
            <td>Condition</td>
            <td>urn:nhs:names:services:flagserver:condition:write</td>
        </tr>
        <tr>
            <td>List</td>
            <td>urn:nhs:names:services:flagserver:list:write</td>
        </tr>
    </tbody>

</table>

