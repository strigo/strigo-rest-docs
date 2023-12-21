---
weight: 1
---

# Introduction

Strigo's v1 REST API allows you to perform most basic actions Strigo supports for non-live interaction with Strigo's
platform.

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
    "https://<STRIGO_ENDPOINT>/api/v1/<endpoint>" [-d <data>]
```

Authentication is done using a Bearer token split into two parts:

* Your organization's unique id.
* Your organization's API key.

Assuming you're an organization's owner, you can generate an API key for your org.
If not, you can retrieve the generated key and org ID.

The creds can be found [here](https://app.strigo.io/settings#account).

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
    "type": "ClassNotFound",
    "message": "Class hd3ALTaLAbhfzmBbf could not be found."
  }
}
```

Each response, (except for `/health`) contains at the very least one high-level key (`result`) and two optional
ones (`data` and `error`).

<aside class="notice">
Successful `DELETE` requests do not return a structured response, and instead return a 204 (No Content) status code.
</aside>

### The `result` Key

The `result` key is supposed to help you identify, before proceeding any further in your code, whether the request was
successful or not. This is merely a convenience. The values can either be `success` or `failure`.

### The `data` Key

The `data` key is only included when we need to return any data to act on. `DELETE` actions, for example,
don't return data.

### The `error` Key

The `error` key is only included when an error occurs, and has two fields (`type` and `message`).

* `type` -> The Strigo-specific type of error (e.g. `ClassNotFound`). While you can operate on HTTP status codes, this
  provides a more elaborate mechanism for acting on errors. For example, a request can return `400` for two completely
  different types of errors.
* `message` -> A more elaborate, human-readable message describing the error.

Request validation errors also return an `errors` array as part of the error:

```json
{
  "result": "failure",
  "error": {
    "message": "The request is not valid",
    "type": "RequestValidationError",
    "errors": [
      {
        "location": "body",
        "param": "class_id",
        "msg": "Must be a valid class ID"
      },
      {
        "location": "body",
        "param": "owner",
        "msg": "Must be a valid email address"
      },
      {
        "location": "body",
        "param": "date_start",
        "msg": "Must be an ISO8601 compliant date"
      },
      {
        "location": "body",
        "param": "date_end",
        "msg": "Must be an ISO8601 compliant date"
      }
    ]
  }
}
```

<aside class="notice">
All responses shown in the examples in the API reference only include the content of the `data` key in the response.
</aside>

## Errors and Validations

### Validation errors

Request validations are performed on all request query and body parameters. This should allow users to understand
exactly which parameter is invalid.

For all validation errors, the `RequestValidationError` error type is returned with HTTP error 422.

### Granular Error Types (WIP)

We provide rather granular error types that should allow you to programmatically respond to errors.

For example, given a DELETE request to delete an event that is currently live, an `EventNotInReadyState` error type will
be returned.

### Error Codes

We use standard response codes for all requests.

## Actions and Methods

We use the common pattern of performing actions based on the HTTP method used:

* `GET` for retrieving a list of entities or a single entity.
* `POST` for creating a new entity.
* `PATCH` for updating an existing entity.
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
  "status": "ok",
  "message": "Healthy"
}
```

### Endpoint

`GET /health`

### Usage

This can be used to verify server integrity and to validate your credentials.

## Rate Limiting

We currently allow ~1xx-~2xx RPM. This will change in the future.

All responses contain headers indicating the current limit status.


> Response Example

```shell
HTTP/1.1 201 Created
connection: keep-alive
content-length: 176
content-type: application/json; charset=utf-8
date: Sun, 28 Oct 2018 08:14:55 GMT
etag: W/"b0-oyLnTncCdwzOLaMEktxD6NJ1PL0"
vary: Accept-Encoding
x-powered-by: Express
x-ratelimit-limit: 60
x-ratelimit-remaining: 59
x-ratelimit-reset: 1540714538

...
```

> Passed the limit

```shell
HTTP/1.1 429 Too Many Requests
connection: keep-alive
content-length: 42
content-type: text/html; charset=utf-8
date: Sun, 28 Oct 2018 08:37:49 GMT
etag: W/"2a-UpTsLJ74nYuiLgNgEwlQMxGqwrE"
retry-after: 60
vary: Accept-Encoding
x-powered-by: Express
x-ratelimit-limit: 60
x-ratelimit-remaining: 0
x-ratelimit-reset: 1540715901

Too many requests, please try again later.
```

