---
title: Endpoints
keywords: usecase
tags: [rest, fhir, identification, development]
sidebar: accessrecord_rest_sidebar
permalink: design_endpoints.html
summary: Endpoints describes the endpoints and methods supported by the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## Endpoints ##

    
The Reasonable Adjustments API offers the following Endpoints and Methods using the standard [FHIR ReST paradigm](http://hl7.org/fhir/STU3/http.html)
    
### /Consent ###

- Read/GET
```
GET [baseUrl]/Consent?
      patient=[nhs#]&status=active&category=RAFlag /HTTP1.1
```

*request payload:*
    none

*response:*
     searchset bundle containing 0..1 Consent resource

- Create/POST
```
POST [baseUrl]/Consent  /HTTP1.1
```

*request payload:*
    a CareConnect-RARecord-Consent-1 resource

*response:*
    201 Created http response code and Location header (and mirror POSTed payload)  
(or operation outcome if failure to find or process) 

- Update(Delete)/PUT
```
PUT [baseUrl]/Consent/[id] /HTTP1.1
```

*request payload:*
    a CareConnect-RARecord-Consent-1 resource

*response:*
200 OK http response code (and mirror PUT payload)  
(or operation outcome if failure to find or process)


### /Flag ###

- Read/GET
```
GET [baseUrl]/Flag?
      patient=[nhs#]&status=active&category=RAFlag /HTTP1.1
```

*request payload:*
    none

*response:*
     searchset bundle containing 0..1 Flag resource

- Create/POST
```
POST [baseUrl]/Flag  /HTTP1.1
```

*request payload:*
    a CareConnect-RARecord-Flag-1 resource

*response:*
    201 Created http response code and Location header (and mirror POSTed payload)  
(or operation outcome if failure to find or process) 

- Update(Delete)/PUT
```
PUT [baseUrl]/Flag/[id] /HTTP1.1
```

*request payload:*
    a CareConnect-RARecord-Flag-1 resource

*response:*
200 OK http response code (and mirror PUT payload)  
(or operation outcome if failure to find or process)

The Reasonable Adjustments API also offers the following additional Endpoints and Methods. These do not follow standard FHIR ReST patterns - they are generically standard ReSTful - but are pragmatically offered in order to simplify integration.


### /List ###

- Read/GET
```
GET [baseUrl]/List?
      patient=[nhs#]&status=active&category=RAFlag /HTTP1.1
```

*request payload:*
    none

*response:*
     searchset bundle containing 0..1 List resource

- Create/POST
```
POST [baseUrl]/List  /HTTP1.1
```

*request payload:*
    a CareConnect-RARecord-List-1 resource

*response:*
    201 Created http response code and Location header (and mirror POSTed payload)  
(or operation outcome if failure to find or process) 

- Update(Delete)/PUT
```
PUT [baseUrl]/List/[id] /HTTP1.1
```

*request payload:*
    a CareConnect-RARecord-List-1 resource

*response:*
200 OK http response code (and mirror PUT payload)  
(or operation outcome if failure to find or process)

### /UnderlyingConditions ###

- Read/GET
```
GET [baseUrl]/UnderlyingConditions?
      patient=[nhs#]&status=active&category=RAFlag /HTTP1.1
```

*request payload:*
    none

*response:*
     searchset bundle containing 0..1 List resource

- Create/POST
```
POST [baseUrl]/UnderlyingConditions  /HTTP1.1
```

*request payload:*
    a CareConnect-RARecord-List-1 resource

*response:*
    201 Created http response code and Location header (and mirror POSTed payload)  
(or operation outcome if failure to find or process) 

- Update(Delete)/PUT
```
PUT [baseUrl]/UnderlyingConditions/[id] /HTTP1.1
```

*request payload:*
    a CareConnect-RARecord-List-1 resource

*response:*
200 OK http response code (and mirror PUT payload)  
(or operation outcome if failure to find or process)

### /ThresholdCode ###

- Read/GET
```
GET [baseUrl]/ThresholdCode?
      patient=[nhs#]&status=active&category=RAFlag /HTTP1.1
```

*request payload:*
    none

*response:*
     searchset bundle containing 0..1 Condition resource