---
title: Interaction | Read
keywords: usecase
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_usecases_additional.html
summary: Describes additional examples of resource instances to illustrate acceptable implementation of the Resource Profile StructureDefinitions.
---
{% include custom/search.warnbanner.html %}

# Additional Examples #

These examples illustrate the resource representation of several different approaches to capture Reasonable Adjustment detail.
They could represent:
- the resources persisted on the FHIR Server holding the Reasonable Adjustment Flag record
- alternative payloads for Read requests for different scenarios

## 1. A patient with multiple Reasonable Adjustments within the same Category ##

+ Reasonable Adjustment Category: Communication Needs  
+ Reasonable Adjustment 1: Provide written reminders and advice  
  - RARecord-Flag-1-example-2
+ Reasonable Adjustment Category: Communication Needs  
+ Reasonable Adjustment 2: Adjust for use of communication book / aid  
  - RARecord-Flag-1-example-3

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-2.xml"
title="RARecord-Flag-1-example-2"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-2.json"
title="RARecord-Flag-1-example-2"
type="json" %}

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-3.xml"
title="RARecord-Flag-1-example-3"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-3.json"
title="RARecord-Flag-1-example-3"
type="json" %}

## 2. A patient with multiple Reasonable Adjustments but fall under different Categories; ##
            
+ Reasonable Adjustment Category: Environment  
+ Reasonable Adjustment: Adjust / minimise waiting times  
  - RARecord-Flag-1-example-4

+ Reasonable Adjustment Category: Specific Risks  
+ Reasonable Adjustment: Monitor for epilepsy  
  - RARecord-Flag-1-example-5

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-4.xml"
title="RARecord-Flag-1-example-4"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-4.json"
title="RARecord-Flag-1-example-4"
type="json" %}

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-5.xml"
title="RARecord-Flag-1-example-5"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-5.json"
title="RARecord-Flag-1-example-5"
type="json" %}

## 3. A patient with a Reasonable Adjustment which contains a Reasonable Adjustment Code plus additional detail (free text) ##

+ Reasonable Adjustment Category: Individual Care Requirements  
+ Reasonable Adjustment: Consider adjustment to provide Female only support  
+ Supporting detail (free text): Patient becomes anxious when treated by Male staff  
  - RARecord-Flag-1-example-6

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-6.xml"
title="RARecord-Flag-1-example-6"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-6.json"
title="RARecord-Flag-1-example-6"
type="json" %}

## 4. A patient with a Reasonable Adjustment which is entirely free text i.e. a Generic reasonable adjustment ##

+ Reasonable Adjustment Category: Generic Reasonable Adjustment  
+ Supporting Detail (free text): Patient struggles to communicate directly however carries a toy with them, experience has shown communicating through the toy to explain issues and required procedures helps the patient feel more at ease and digest the information  
  - RARecord-Flag-1-example-7

{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-7.xml"
title="RARecord-Flag-1-example-7"
type="xml" %}
{% include custom/fhir.codegrid.html
relfilepath="usecaseexamples/RARecord-Flag-1-example-7.json"
title="RARecord-Flag-1-example-7"
type="json" %}
