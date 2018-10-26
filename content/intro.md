---
weight: 1
---

# Introduction

Strigo's v1 REST API allows you to perform most basic actions Strigo supports for non-live interaction with Strigo's platform.

Some actions, like changing billing settings, are only available via the web interface.


<aside class="notice">
This section describes various API features that apply to all resources
</aside>

## API Endpoint

The default API endpoint for all v1 requests is:

`https://app.strigo.io/api/v1`

All paths shown here are relative to this path.


## Authentication

> Basic usage

```shell
$ curl -X METHOD \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "http://<STRIGO_ENDPOINT>/api/v1/<endpoint>" [-d <data>]
```

Authentication is done using a Bearer token split into two parts:

* Your organization's unique id.
* Your organization's API key.

Assuming you're an organization's owner, you can generate an API key for your org.
If not, you can retrieve the generated key and org ID.

The creds can be found [here](http://app.strigo.io/settings#account).

We'll be adding additional authentication methods in the future.


## Response Structure

> Successful Request Response Example

```json
{
  "result": "success",
  "data": [
    {
      "level": "owner",
      "email": "user1@strigo.io",
      "id": "rMWNrMT2PCySh2PSo"
    },
    {
      "level": "member",
      "email": "user2@strigo.io",
      "id": "AsEM3RtnbuudJBLD5"
    }
  ]
}
```

> Failed Request Response Example

```json
{
  "result": "failure",
  "error": {
    "type": "classNotFound",
    "message": "Class hd3ALTaLAbhfzmBbf could not be found."
  }
}
```

Each response, (except for `/health`) contains at the very least one high-level key (`result`) and two optional ones (`data` and `error`).

### The `result` Key

The `result` key is supposed to help you identify, before proceeding any further in your code, whether the request was successful or not. This is merely a convenience.

### The `data` Key

The `data` key is only included when we need to return any data to act on. `DELETE` actions, for example,
don't return data.

### The `error` Key

The `error` key is only included when an error occurs, and has two fields (`type` and `message`).

* `type` -> The Strigo-specific type of error (e.g. `classNotFound`). While you can operate on HTTP status codes, this provides a more elaborate mechanism for acting on errors. For example, a request can return `400` for two completely different types of errors.
* `message` -> A more elaborate, human-readable message describing the error.

<aside class="notice">
All responses shown in the examples in the API reference only include the content of the `data` key in the response.
</aside>

## Actions and Methods

Strigo uses the common pattern of performing actions based on the HTTP method used:

* `POST` for creating a new entity.
* `GET` for retrieving a list of entities or a single entity.
* `PATCH/PUT` for updating an existing entity.
* `DELETE` for deleting an entity.



## Health Check

> Request

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/health"
```

> Response

```json
{
  "status":"ok",
  "message":"Healthy"
}
```

### Endpoint

`GET /health`

### Usage

This can be used to verify server integrity and to validate your credentials.
