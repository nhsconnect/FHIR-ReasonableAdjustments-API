---
title: Interaction | Caching and Managing Updates
keywords: usecase, CareConnect-RARecord-Condition-1
tags: [rest, fhir, identification,development]
sidebar: accessrecord_rest_sidebar
permalink: design_resource_contention.html
summary: How resources updates are managed to allow local caching, and to avoid contention when updating resources
---
{% include custom/search.warnbanner.html %}

## 1. Resource Versioning ##

To facilitate the management of [resource contention](http://hl7.org/fhir/http.html#concurrency), all resources returned will include a version ID.

The version ID is specified in the "meta" section of the resource - for example:

```
<Flag xmlns="http://hl7.org/fhir">
	<id value="744eec7d-8951-4722-ad74-dc34e86d4e1a"/>
	<meta>
		<versionId value="25777f7d-27bc"/>
		<profile value="https://fhir.nhs.uk/STU3/StructureDefinition/RARecord-Flag-1"/>
	</meta>
	<!-- Flag resource content -->
</Flag>
```

The version ID value is specific to the version of the flag (in the above example: **25777f7d-27bc**), and will change every time this specific flag resource is updated (the resource ID in the "id" field will remain the same). The version ID can be any value valid as per the [id datatype](https://www.hl7.org/fhir/datatypes.html#id), and may not be a sequential number - clients should not infer any specific meaning on the values of the ID.

Resources returned in a bundle will each have their own ID and versionID values within the resource, but in addition, where a client does a READ on an individual resource by ID, the versionID for the resource will also be returned in an ETag HTTP header:

```
HTTP 200 OK
Date: Sat, 09 Feb 2013 16:09:50 GMT
ETag: W/"25777f7d-27bc"
Content-type: application/json+fhir

... Resource content as above ...
```

ETag headers which denote resource version IDs SHALL be prefixed with W/ and enclosed in quotes, for example:

```
ETag: W/"25777f7d-27bc"
```

NOTE: The above does not mean that the API provides access to older versions of resources - the versionID for older versions of a resource are not made available (for example through a VREAD operation).

## 2. Caching READs ##

When a client does a READ operation to access a specific resource by ID, it may choose to include an ```If-None-Match``` header to specify the version ID of the latest version they have of that resource - for example:

```
GET /Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a
If-None-Match: W/"25777f7d-27bc"
```

If the version ID specified in the HTTP header matches the latest held on Spine, a HTTP 304 Not Modified status code will be returned to inform the client that they already have the latest version:

```
HTTP/1.1 304 Not Modified
Date: Mon, 18 Sep 2015 22:20:01 GMT
```

If a newer version of the resource does exist, it will be returned as normal, with the newer versionID as described above so the client can update its cache.

## 3. Managing Updates

There is a risk in some cases that two clients will try to update the same resource. If both clients had the same version of that resource to begin with, there is a risk that and the second overwrites the updates of the first. To prevent this happening, clients MUST submit update requests with an If-Match header that quotes the ETag from the server. This specified the version of the resource that their updates should be applied to, so a second attempt to update the same version with different changes can be detected as a conflict and rejected (this is also known as optimistic locking).

Updates would include the versionID in the HTTP header as follows:

```
PUT /Flag/744eec7d-8951-4722-ad74-dc34e86d4e1a
If-Match: W/"25777f7d-27bc"
```

If the version Id given in the If-Match header does not match, the server returns a 409 Conflict status code instead of updating the resource.

