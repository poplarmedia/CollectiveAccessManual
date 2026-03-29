---
title: Simple API
sidebar_position: 4
---
# Simple API

Contrary to the "main" [JSON API](web_service.md) this simpler
interface puts the payload formatting configuration for a service call
in a config file on the CollectiveAccess server. This allows for much
simpler client-side code and also means you can change the returned
format without changing the client code (which could mean having to
recompile and going through App Store approval again, etc.). The
server-side configuration is done using [Display Templates](../../reporting/display_templates.md).

## Example

- Edit API endpoints in `app/conf/services.conf`, for example like this:

<!-- -->

```
template_api_endpoints = {
    testDetail = {
        type = detail,
        table = ca_objects,
        restrictToTypes = [image,dataset],
        checkAccess = [1,2],
        content = {
            object_id = ^ca_objects.object_id,
            display_label = ^ca_objects.preferred_labels
        }
    },
    testSearch = {
            type = search,
            table = ca_objects,
            content = {
                object_id = ^ca_objects.object_id,
                display_label = ^ca_objects.preferred_labels
            }
        }
}
```

- [Authenticate](web_service.md#authentication) using the JSON API authentication method.

- Query either

```
  http://localhost/service.php/simple/<your_endpoint>?id=<id_or_idno>&pretty=1
```

  for detail pages or

```
  http://localhost/service.php/simple/<your_endpoint>?q=*&pretty=1
```

  for search endpoints.

## Authentication

The authentication code is shared with the JSON API, so please refer to the respective section in the [JSON API documentation](web_service.md#authentication). **Note that you should not use your admin or every-day user account and unencrypted HTTP basic auth to access the service API!** It's okay to do so while developing on a local machine, which is why some of the examples below include plaintext user/pw combinations.

If you're operating remotely on a production system however, you should look into token-based authentication, a separate API user account that doesn't have permissions to do anything else, and most importantly, TLS encryption.

## Usage and configuration

Each service call refers to what we call an "endpoint". A system can have an arbitrary number of simple service endpoints. They are configurable in `app/conf/services.conf` and are called by sending a simple GET request to:

```
http://localhost/service.php/simple/<your_endpoint>
```

There are two different types of simple services: **detail** is used to get detailed information about a specific record identified by either its primary key or its idno. **search** can be used to run basic searches and return information about a list of records. Both have an additional mandatory GET parameter that must be passed to the endpoint:

| Service type | Parameter | Values | Description |
|---|---|---|---|
| search | q | string | Search query |
| detail | id | integer or short string | Primary key |
| all | pretty | 0 or 1 | Format returned JSON for readability *(parameter is optional)* |
| all | noCache | 0 or 1 | If set to 1, result is always pulled from the database and not from a local cache. Can be handy when developing configurations. |
| search | returnDataAsList | 0 or 1 | If set to 1, search result data is returned as a list under the key "data", rather than as key/value pairs in the response hash. This option is useful when maintaining the order of returned results is important, as the JSON specification only guarantees maintenance of order for lists. **Available from version 1.7** |

The endpoint configuration is in the `simple_api_endpoints` array in `app/conf/services.conf`. You can have an arbitrary number of endpoints. Each endpoint refers to a specific kind of record (objects, entities, occurrences, etc.) and can optionally be restricted by type. It also defines a list of key value pairs that are returned in the service response if that endpoint is queried.

The settings for an endpoint are as follows:

| Setting | Description | Example |
|---|---|---|
| type | Type of service endpoint. Can be "search" or "detail". | detail |
| table | What kind of record should this endpoint return information for? Should refer to one of the CollectiveAccess primary tables. | ca_objects |
| restrictToTypes | Optional list of type restrictions for this service. Can be useful if you want to tailor an endpoint towards a specific type of record (e.g. persons/individuals), and don't want it to be used for other records in the same class (e.g. organizations) | [image,dataset] |
| checkAccess | Optional list of access restrictions for this service. If set, records with access values not in that list won't show up, at least for the primary service "target". You can potentially still pull in non-accessible related records. | [1,2] |
| content | List of key value pairs that are part of the service response for this endpoint. Each value must be a valid [Display Template](../../reporting/display_templates.md) that is then run against the current record or against each record in the result set. | |

A valid minimal example is in the Example section above.

If you have that configuration set up, you could run a simple query like this to get details for the object with primary key (object_id) 33:

```
$ curl -XGET 'http://user:password@localhost/service.php/simple/testDetail?id=33&pretty=1'
```

Note the endpoint name "testDetail". The result would be:

```json
{
  "ok": true,
  "object_id": "1",
  "display_label": "asdf"
}
```

The "ok" key is always present and indicates if there was an error while processing the request.