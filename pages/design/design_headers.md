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
* InteractionID: [serviceName]

[InteractionID](/design_headers.html#interactionid) varies by resource and interaction undertaken.

#### Update requests ####
* If-Match: [versionIdETag]

### Responses ###

#### All Read & failure responses ####
* Date: [servedNowDate]
* Content-type: application/json+fhir or application/xml+fhir

#### All successful Create responses ####
* Date: [servedNowDate]
* Last-Modified: [lastModDate]
* Location: https://clinicals.spineservices.nhs.uk/STU3/[type]/[id]/_history/[vid]
* ETag: W/"[versionId]"
* Content-type: application/json+fhir or application/xml+fhir

#### All successful Update responses ####
* Date: [servedNowDate]
* Last-Modified: [lastModDate]
* ETag: W/"[versionId]"
* Content-type: application/json+fhir or application/xml+fhir


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
            <td>urn:nhs:names:services:flagserver:consent:update</td>
        </tr>
        <tr>
            <td>Flag</td>
            <td>urn:nhs:names:services:flagserver:flag:update</td>
        </tr>
        <tr>
            <td>Condition</td>
            <td>urn:nhs:names:services:flagserver:condition:update</td>
        </tr>
        <tr>
            <td>List</td>
            <td>urn:nhs:names:services:flagserver:list:update</td>
        </tr>
    </tbody>

</table>

