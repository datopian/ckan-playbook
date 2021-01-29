Note that you can access official CKAN docs here: https://docs.ckan.org/

This repository provides examples of CKAN APIs usage for various scenarios.

## Package API

All requests should:

* use base url `https://your-ckan-domain.com/api/3/action/`
* use POST method;
* set `Content-Type` header to `application/json`;
* set `Authorization` header with your API key.

### Create

Endpoint: `/package_create`.

Request body example:

```json
{
  "name": "test-dataset",
  "title": "Test dataset",
  "private": false,
  "author": "Name Surname 1",
  "author_email": "name.surname1@example.com",
  "maintainer": "Name Surname 2",
  "maintainer_email": "name.surname2@example.com",
  "notes": "This is a description of a test dataset.",
  "owner_org": "name-or-id-of-an-owner-org"
}
```

Note that there are many other optional metadata attributes you may want to use. See https://docs.ckan.org/en/2.9/api/index.html#ckan.logic.action.create.package_create.

Response example:

```json
{
  "help": "http://127.0.0.1:5000/api/3/action/help_show?name=package_create",
  "success": true,
  "result": {
    "license_title": null,
    "maintainer": "Name Surname 2",
    "relationships_as_object":[],
    "private": false,
    "maintainer_email": "name.surname2@example.com",
    "num_tags": 0,
    "id": "0686b84b-bfed-45dd-8bb9-42ebc80cf2d3",
    "metadata_created": "2021-01-26T12:27:47.920317",
    "metadata_modified": "2021-01-26T12:27:47.920324",
    "author": "Name Surname 1",
    "author_email": "name.surname1@example.com",
    "state": "active",
    "version": null,
    "creator_user_id": "a29f9229-119d-4638-adf1-6e38da43d97e",
    "type": "dataset",
    "resources":[],
    "num_resources": 0,
    "tags":[],
    "groups":[],
    "license_id": null,
    "relationships_as_subject":[],
    "organization": {
      "description": "",
      "created": "2021-01-26T12:27:36.251113",
      "title": "name-or-id-of-an-owner-org"
    },
    "name": "test-dataset",
    "isopen": false,
    "url": null,
    "notes": "This is a description of a test dataset.",
    "owner_org": "db40255d-0a2e-4b5f-87b3-2b9d4ecdee85",
    "extras":[],
    "title": "Test dataset",
    "revision_id": "9b509af8-8c80-48c1-b9d6-d1cc2e5d9400"
  }
}
```

### Update

Endpoint: `/package_update`.

Request body example (`id` can be either name or id of a package):

```json
{
  "id": "test-dataset",
  "title": "Test dataset",
  "private": false,
  "author": "Name Surname 1",
  "author_email": "name.surname1@example.com",
  "maintainer": "Name Surname 2",
  "maintainer_email": "name.surname2@example.com",
  "notes": "This is a description of a test dataset.",
  "owner_org": "name-or-id-of-an-owner-org"
}
```

Note that there are many other optional metadata attributes you may want to use. See https://docs.ckan.org/en/2.9/api/index.html#ckan.logic.action.update.package_update.

Response example:

```json
{
  "help": "http://127.0.0.1:5000/api/3/action/help_show?name=package_update",
  "success": true,
  "result":{
    "license_title": null,
    "maintainer": "Name Surname 2",
    "relationships_as_object":[],
    "private": false,
    "maintainer_email": "name.surname2@example.com",
    "num_tags": 0,
    "id": "0686b84b-bfed-45dd-8bb9-42ebc80cf2d3",
    "metadata_created": "2021-01-26T12:27:47.920317",
    "metadata_modified": "2021-01-26T12:41:56.478594",
    "author": "Name Surname 1",
    "author_email": "name.surname1@example.com",
    "state": "active",
    "version": null,
    "creator_user_id": "a29f9229-119d-4638-adf1-6e38da43d97e",
    "type": "dataset",
    "resources":[],
    "num_resources": 0,
    "tags":[],
    "groups":[],
    "license_id": null,
    "relationships_as_subject":[],
    "organization":{
      "description": "",
      "created": "2021-01-26T12:27:36.251113",
      "title": "name-or-id-of-an-owner-org"
    },
    "name": "test-dataset",
    "isopen": false,
    "url": null,
    "notes": "This is a description of a test dataset.",
    "owner_org": "db40255d-0a2e-4b5f-87b3-2b9d4ecdee85",
    "extras":[],
    "title": "Test dataset 2",
    "revision_id": "8d28cf4d-ef6c-4747-a65e-fb6fbfd7fef8"
  }
}
```

## Resource API

All requests should:

* use base url `https://your-ckan-domain.com/api/3/action/`
* use POST method;
* set `Content-Type` header to `application/json`;
* set `Authorization` header with your API key.

### Create

Endpoint: `/resource_create`.

Request body example (`package_id` is an id or name of a package which this resource belongs to):

```json
{
  "package_id": "test-dataset",
  "url": "https://www.example.com/data.csv",
  "description": "Test resource title",
  "format": "CSV",
  "name": "test-resource"
}
```

or you may also upload a file into storage (e.g., S3 bucket). Note that in this case you need to use `multipart-form-data`, for example, using `curl`:

```
curl -H'Authorization: your-api-key' 'http://127.0.0.1:5000/api/3/action/resource_create' --form upload=@pathtofile --form package_id=my_dataset
```

Note that there are many other optional metadata attributes you may want to use. See https://docs.ckan.org/en/2.9/api/index.html#ckan.logic.action.create.resource_create.

Response example:

```json
{
  "help": "http://127.0.0.1:5000/api/3/action/help_show?name=resource_create",
  "success": true,
  "result":{
    "cache_last_updated": null,
    "cache_url": null,
    "mimetype_inner": null,
    "hash": "",
    "description": "Test resource title",
    "format": "CSV",
    "url": "https://www.example.com/data.csv",
    "created": "2021-01-26T12:48:41.789301",
    "state": "active",
    "package_id": "0686b84b-bfed-45dd-8bb9-42ebc80cf2d3",
    "last_modified": null,
    "mimetype": null,
    "url_type": null,
    "position": 0,
    "revision_id": "4fcdab1b-eca7-4aa7-81e1-5472c554bb59",
    "size": null,
    "datastore_active": false,
    "id": "8680277d-aaef-4979-8b46-56412e2f16d7",
    "resource_type": null,
    "name": "test-resource"
  }
}
```

### Update

Endpoint: `/resource_update`.

Request body example (`id` is an id of a resource which can be retrieved from the response of `resource_create` action):

```json
{
  "id": "8680277d-aaef-4979-8b46-56412e2f16d7",
  "url": "https://www.example.com/data.csv",
  "description": "Updated resource title",
  "format": "CSV",
  "name": "updated-test-resource"
}
```

Note that there are many other optional metadata attributes you may want to use. See https://docs.ckan.org/en/2.9/api/index.html#ckan.logic.action.update.resource_update.

Response example:

```json
{
  "help": "http://127.0.0.1:5000/api/3/action/help_show?name=resource_update",
  "success": true,
  "result": {
    "cache_last_updated": null,
    "cache_url": null,
    "mimetype_inner": null,
    "hash": "",
    "description": "Updated resource title",
    "format": "CSV",
    "url": "https://www.example.com/data.csv",
    "created": "2021-01-26T12:48:41.789301",
    "state": "active",
    "package_id": "0686b84b-bfed-45dd-8bb9-42ebc80cf2d3",
    "last_modified": null,
    "mimetype": null,
    "url_type": null,
    "position": 0,
    "revision_id": "41a41a9a-c795-44cd-8c0c-6be1d03d305a",
    "size": null,
    "datastore_active": false,
    "id": "8680277d-aaef-4979-8b46-56412e2f16d7",
    "resource_type": null,
    "name": "updated-test-resource"
  }
}
```

### Patch

Endpoint: `/resource_patch`.

Request body example:

```json
{
  "id": "8680277d-aaef-4979-8b46-56412e2f16d7",
  "description": "Only update needed attribute."
}
```

Note that there are many other optional metadata attributes you may want to use. See https://docs.ckan.org/en/2.9/api/index.html#ckan.logic.action.patch.resource_patch.

Response example:

```json
{
  "help": "http://127.0.0.1:5000/api/3/action/help_show?name=resource_patch",
  "success": true,
  "result": {
    "cache_last_updated": null,
    "cache_url": null,
    "mimetype_inner": null,
    "hash": "",
    "description": "Only update needed attribute.",
    "format": "CSV",
    "url": "https://www.example.com/data.csv",
    "created": "2021-01-26T12:48:41.789301",
    "state": "active",
    "package_id": "0686b84b-bfed-45dd-8bb9-42ebc80cf2d3",
    "last_modified": null,
    "mimetype": null,
    "url_type": null,
    "position": 0,
    "revision_id": "b62edbe3-e2b2-41e6-815e-f9adf70a66aa",
    "size": null,
    "datastore_active": false,
    "id": "8680277d-aaef-4979-8b46-56412e2f16d7",
    "resource_type": null,
    "name": "updated-test-resource"
  }
}
```
