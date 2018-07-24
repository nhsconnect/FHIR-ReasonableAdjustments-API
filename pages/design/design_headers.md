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
* InteractionID: urn:nhs:names:services:flagserver

#### Update requests ####
* If-Match: [versionIdETag]

### Responses ###

#### All failure responses ####
* Date: [servedNowDate]

#### All success responses ####
* Date: [servedNowDate]
* Last-Modified: [lastModDate]
* ETag: W/"[versionId]"
* Content-type: application/json+fhir or application/xml+fhir

#### Create responses ####
* Location: https://clinicals.spineservices.nhs.uk/STU3/[type]/[id]/_history/[vid]