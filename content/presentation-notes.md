---
weight: 109
---


# Presentation Notes

<aside class="notice">
Currently, there's no way to handle single notes. You can only GET, POST or DELETE all notes in a single call.
</aside>

## The Presentation Notes Resource

Attribute     | Type     | Description
---------     | -------  | -------
`notes`       | List     | A list of Note objects.


## Retrieve all notes

> Request Example

```shell
$ curl -X GET \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/RXKeXmMBjptt3EMQt/presentations/455e6c87af85c916d9bc2e7c/notes"
```

> Response Example

```json
[
  {
      "content": "yo",
      "page": 1
  }
]
```

### Usage

Lists all presentation notes for your presentation.

`GET "/classes/:class_id/presentations/:presentation_id/notes"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.
`presentation_id` | String | Yes | The presentation's unique identifier.


## Create notes for a presentation

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/RXKeXmMBjptt3EMQt/presentations/455e6c87af85c916d9bc2e7c/notes" \
    -d [{"page":"1","content":"yo"}]
```

> Response Example

```json
[
  {
      "content": "yo",
      "page": 1
  }
]
```

### Usage

Assign notes to a presentaiton.

`POST "/classes/:class_id/presentations/:presentation_id/notes"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.
`presentation_id` | String | Yes | The presentation's unique identifier.

### BODY Parameters

Attribute     | Type     | Required | Description
---------     | -------  | -------  | -------
`notes`       | List     | Yes      | A list of NOTE objects.

### NOTE Parameters

Attribute     | Type     | Required | Description
---------     | -------  | -------  | -------
`page`        | Integer  | Yes      | The page in the presentation to which this note applies.
`content`     | String   | Yes      | The textual content of the note.


## Delete all notes for a presentation

> Request Example

```shell
$ curl -X DELETE \
    -H "Authorization: Bearer ${ORG_ID}:${API_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://app.strigo.io/api/v1/classes/RXKeXmMBjptt3EMQt/presentations/455e6c87af85c916d9bc2e7c/notes"
```

> Response Example

```json
{
  "result": "success"
}
```

### Usage

Delete all notes for a presentation.

`DELETE "/classes/:class_id/presentations/:presentation_id/notes"`

### URL Parameters

Attribute  | Type    | Required | Description
---------  | ------- | -------  | -------
`class_id` | String  | Yes      | The class's unique identifier.
`presentation_id` | String | Yes | The presentation's unique identifier.
