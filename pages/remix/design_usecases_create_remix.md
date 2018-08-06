---
title: Interaction | Create
keywords: usecase
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_create_remix.html
summary: Create describes the interaction required to record a new Reasonable Adjustment Flag, an Adjustment or an Impairment on Spine via the FHIR&reg; Reasonable Adjustments API
---
{% include custom/search.warnbanner.html %}

## 1 Create RA Record ##

#### Trigger: ####
* GP initiates Reasonable Adjustment Flag discussion at annual health check 

#### System Scope: ####
* ClientSystem includes Acute/DepartmentalSystem client, SCRa, 1-click etc.  
* ServerSystem includes Spine, PDS, SDS, FlagServer etc.  

#### Summary: ####
Practitioner creates RARecord, recording Consent from Patient and that Impairment is 'Learning Disability'.  
Patient declines to record a specific Adjustment at this time.  

#### Pre ####
* Patient arrives at check  
* Practitioner logged into ClientSystem, traces & verifies demographic information
* Practitioner searches for Patient's RARecord
  * ClientSystem searched and failed to find existing RARecord [(see Use Case Initial Read Failure)](/design_usecases_remix.html#1-initial-read-failure---no-ra-record)
* Practitioner discusses RARecord with Patient  

#### Main ####
* Patient consents to record RA Flag  
  * Practitioner creates new RARecord for Patient (by recording Consent)  
  * Practitioner records Patient consented to record RA info  
    * ClientSystem captures and structures Consent information as new RARecord-Consent-1 resource [(xml)](design_usecases_create_remix.html#21-new-consent-resource---xml-example) [(json)](design_usecases_create_remix.html#22-new-consent-resource---json-example)

* Patient agrees to record 'Learning Disability' as Impairment  
  * Practitioner adds Impairment from coded picklist (optionally elaborates w separate freetext)  
    * ClientSystem captures and structures Impairment information as new Impairment (CareConnect-RARecord-Condition-1) resource [(xml)](design_usecases_create_remix.html#23-new-impairment-resource---xml-example) [(json)](design_usecases_create_remix.html#24-new-impairment-resource---json-example)

* Patient declines to record any specific Adjustments at this time

* Practitioner commits RARecord  
    * ClientSystem submits Create Consent request [(xml)](design_usecases_create_remix.html#31-create-consent-request---xml-example) [(json)](design_usecases_create_remix.html#32-create-consent-request---json-example)
      * ServerSystem submits Create Consent response [(xml)](design_usecases_create_remix.html#33-create-consent-response---xml-example) [(json)](design_usecases_create_remix.html#34-create-consent-response---json-example)
    * ClientSystem submits Create Condition request [(xml)](design_usecases_create_remix.html#35-create-condition-request---xml-example) [(json)](design_usecases_create_remix.html#36-create-condition-request---json-example)
      * ServerSystem submits Create Condition response [(xml)](design_usecases_create_remix.html#37-create-condition-response---xml-example) [(json)](design_usecases_create_remix.html#38-create-condition-response---json-example)
        * ClientSystem creates new CareConnect-RARecord-List-1 to reference / identify Impairment resource  [(xml)](design_usecases_create_remix.html#25-new-list-resource---xml-example) [(json)](design_usecases_create_remix.html#26-new-list-resource---json-example)
    * ClientSystem submits Create List request [(xml)](design_usecases_create_remix.html#39-create-list-request---xml-example) [(json)](design_usecases_create_remix.html#310-create-list-request---json-example)
      * ServerSystem submits Create List response [(xml)](design_usecases_create_remix.html#311-create-list-response---xml-example) [(json)](design_usecases_create_remix.html#312-create-list-response---json-example)

---

### 2.1 New Consent Resource - xml example ###
### 2.2 New Consent Resource - json example ###
### 2.3 New Impairment Resource - xml example ###
### 2.4 New Impairment Resource - json example ###
### 2.5 New List Resource - xml example ###
### 2.6 New List Resource - json example ###


### 3.1 Create Consent Request - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Create Consent Request"
type="xml" %}


### 3.2 Create Consent Request - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Create Consent Request"
type="json" %}


### 3.3 Create Consent Response - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Create Consent Response"
type="xml" %}


### 3.4 Create Consent Response - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Create Consent Response"
type="json" %}


### 3.5 Create Condition Request - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Create Condition Request"
type="xml" %}


### 3.6 Create Condition Request - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Create Condition Request"
type="json" %}


### 3.7 Create Condition Response - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Create Condition Response"
type="xml" %}


### 3.8 Create Condition Response - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Create Condition Response"
type="json" %}


### 3.9 Create List Request - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Create List Request"
type="xml" %}


### 3.10 Create List Request - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Create List Request"
type="json" %}


### 3.11 Create List Response - xml example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/xmlExampleFile.xml"
title="Create List Response"
type="xml" %}


### 3.12 Create List Response - json example ###
#### http request & headers ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/[resource]
  HTTP/1.1
Authorization:Bearer [jwt_token_string]
InteractionID:urn:nhs:names:services:flagserver:[resource]:update

```

#### http body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/jsonExampleFile.json"
title="Create List Response"
type="json" %}


---

---
## 1 Create RARecord Use Case ##
#### 1.1 Trigger: ####
GP initiates Reasonable Adjustment Flag discussion at annual health check
#### 1.2 Pre-requisites: ####
Practioner Dr D. logged on w SmartCard/National Identity giving URPId (as SDS OrgPersonRole Identifier)  
Patient Mrs M. PDS Trace > verified NHS#, Name, DoB, demographic data  
ClientSystem searched and failed to find existing RARecord  
#### 1.3 System Scope: ####
ClientSystem includes GPSystem client, SCRa, 1-click etc.  
ServerSystem includes Spine, PDS, SDS, FlagServer etc.  
#### 1.4 Summary: ####
Practitioner creates RARecord, recording Consent from Patient and that Impairment is 'Learning Disability'.  
Patient declines to record a specific Adjustment at this time.  
#### Pre ####
* Patient arrives at check  
* Practitioner opens GPSystem, traces & verifies demographic info (internal call to PDS)  
* Practitioner discusses RARecord with Patient  

#### Main ####
* Patient consents to record RA Flag  
  * Practitioner creates new RARecord for Patient (by recording Consent)  
  * Practitioner records Patient consented to record RA info  
    * ClientSystem captures and structures Consent information as new RARecord-Consent-1 resource  

* Patient agrees to record 'Learning Disability' as Impairment  
  * Practitioner adds Impairment from coded picklist (optionally elaborates w separate freetext)  
    * ClientSystem captures and structures Impairment information as new Impairment (CareConnect-RARecord-Condition-1) resource  
      * ClientSystem creates new CareConnect-RARecord-List-1 to reference / identify Impairment resourcesPatient declines to record any specific RAs  
  * Practitioner commits RARecord  
    * ClientSystem submits Create Consent request  
      * ServerSystem services Create Consent request  
        * ServerSystem submits Create Consent response  
    * ClientSystem submits Create List transaction request  
      * ServerSystem services Create List transaction request  
        * ServerSystem submits Create List transaction response  

## 2 Create RARecord Examples ##
#### 2.1 Create Consent Request ####
#### http request ####
```
POST https://clinicals.spineservices.nhs.uk/STU3/Consent HTTP/1.1
```
#### body ####
Newly created RARecord-Consent-1 resource:
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-CreateConsentRequestBody-example.xml"
title="RARecord-CreateConsentRequestBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-CreateConsentRequestBody-example.json"
title="RARecord-CreateConsentRequestBody-example"
type="json" %}

{% include custom/fhir.header.html %}

Client systems SHALL carry an Access token in the HTTP authorisation header (as an oAuth Bearer Token). See the [API security page](design_security.html) for more details.

#### 2.2 Create Consent Response ####

{% include custom/fhir.response.html %}

#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-CreateConsentResponseBody-example.xml"
title="RARecord-CreateConsentResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-CreateConsentResponseBody-example.json"
title="RARecord-CreateConsentResponseBody-example"
type="json" %}
{% include custom/fhir.header.html %}

#### 2.3 Create List Transaction Request ####
#### http request ####
Transaction handler is at the flagserver base URL
```
POST https://clinicals.spineservices.nhs.uk/STU3 HTTP/1.1
```
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-CreateListTransactionRequestBody-example.xml"
title="RARecord-CreateListTransactionRequestBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-CreateListTransactionRequestBody-example.json"
title="RARecord-CreateListTransactionRequestBody-example"
type="json" %}
{% include custom/fhir.header.html %}

#### 2.4 Create List Transaction Response ####
{% include custom/fhir.response.html %}  
Edge cases TBD and detailed during development
#### body ####
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-CreateListTransactionResponseBody-example.xml"
title="RARecord-CreateListTransactionResponseBody-example"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-CreateListTransactionResponseBody-example.json"
title="RARecord-CreateListTransactionResponseBody-example"
type="json" %}
{% include custom/fhir.header.html %}
