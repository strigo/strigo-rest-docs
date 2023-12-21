---
weight: 106
---

# Presentations

<aside class="notice">
Currently, you can only upload a single presentation per class, and it must be a PDF file.
</aside>

## The Presentation Resource

### Attributes:

| Attribute      | Type     | Description                                                           |
|----------------|----------|-----------------------------------------------------------------------|
| `id`           | String   | The presentation's unique identifier.                                 |
| `class_id`     | String   | The class's unique identifier to which this presentation is assigned. |
| `md5`          | String   | The md5 hash of the presentation.                                     |
| `upload_date`  | Datetime | The date in which the presentation was uploaded.                      |
| `size_bytes`   | Integer  | The size of the file in bytes.                                        |
| `filename`     | String   | The name of the uploaded file.                                        |
| `content_type` | List     | List of types of the file.                                            |

## Retrieve all presentations

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/RXKeXmMBjptt3EMQt/presentations"
```

> Response Example

```json
[
  {
    "id": "455e6c87af85c916d9bc2e7c",
    "md5": "e802201fc6f26d210b07d6da31763ce3",
    "upload_date": "2019-10-17T09:59:44.171Z",
    "size_bytes": 657049,
    "filename": "pres.pdf",
    "content_type": ["application/pdf"],
    "class_id": "RXKeXmMBjptt3EMQt"
  }
]
```

### Usage

Lists all presentations.

`GET "/classes/:class_id/presentations"`

### URL Parameters

| Attribute  | Type   | Required | Description                    |
|------------|--------|----------|--------------------------------|
| `class_id` | String | Yes      | The class's unique identifier. |

## Retrieve a single presentation

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/RXKeXmMBjptt3EMQt/presentations/455e6c87af85c916d9bc2e7c"
```

> Response Example

```json
{
  "id": "455e6c87af85c916d9bc2e7c",
  "md5": "e802201fc6f26d210b07d6da31763ce3",
  "upload_date": "2019-10-17T09:59:44.171Z",
  "size_bytes": 657049,
  "filename": "pres.pdf",
  "content_type": ["application/pdf"],
  "class_id": "RXKeXmMBjptt3EMQt"
}
```

### Usage

Get a single presentation.

<aside class="notice">
This doesn't actually download the presentation. It only displays information about it.
</aside>

`GET "/classes/:class_id/presentations/:presentation_id"`

### URL Parameters

| Attribute         | Type   | Required | Description                           |
|-------------------|--------|----------|---------------------------------------|
| `class_id`        | String | Yes      | The class's unique identifier.        |
| `presentation_id` | String | Yes      | The presentation's unique identifier. |

## Create a presentation

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    "https://app.strigo.io/api/v1/classes/RXKeXmMBjptt3EMQt/presentations" \
    -F 'presentation=@/path/to/pres.pdf'
```

> Response Example

```json
{
  "id": "455e6c87af85c916d9bc2e7c",
  "md5": "e802201fc6f26d210b07d6da31763ce3",
  "upload_date": "2019-10-17T09:59:44.171Z",
  "size_bytes": 657049,
  "filename": "pres.pdf",
  "content_type": ["application/pdf"],
  "class_id": "RXKeXmMBjptt3EMQt"
}
```

### Usage

Uploads a presentation.

`POST "/classes/:class_id/presentations"`

### URL Parameters

| Attribute  | Type   | Required | Description                    |
|------------|--------|----------|--------------------------------|
| `class_id` | String | Yes      | The class's unique identifier. |

### FORM Parameters

| Attribute      | Type | Required | Description                    |
|----------------|------|----------|--------------------------------|
| `presentation` | List | Yes      | A path to a presentation file. |

## Delete a presentation

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/RXKeXmMBjptt3EMQt/presentations/455e6c87af85c916d9bc2e7c"
```

> Response Example

```text
204 No Content
```

### Usage

Delete a presentation.

`DELETE "/classes/:class_id/presentations/:presentation_id"`

### URL Parameters

| Attribute         | Type   | Required | Description                           |
|-------------------|--------|----------|---------------------------------------|
| `class_id`        | String | Yes      | The class's unique identifier.        |
| `presentation_id` | String | Yes      | The presentation's unique identifier. |

